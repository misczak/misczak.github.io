---
categories:
- Cloud Security
date: "2025-10-10T00:00:00Z"
description: Thoughts on the Ruby Central AWS security incident.     
img_path: /assets/img/posts/20251010
pin: false
tags:
- AWS
- Ruby
- Programming
title: About the Ruby Central Security Incident
showTableOfContents: true
---

## Introduction

Recently, Ruby Central, the non-profit responsible for maintaining the RubyGems package manager, suffered a security incident where they temporarily lost control of their AWS account. They have since [published a post-mortem](https://rubycentral.org/news/rubygems-org-aws-root-access-event-september-2025/) of this event that is ostensibly aimed at putting their community's minds at ease. Unfortunately, it had the opposite effect on me, causing me to come away with more questions than  answers. 

## The Incident

Let's begin by looking at the timeline that is included in the post-mortem. All of the events in the initial timeline take place within a few hours on September 30, 2025. Three particular entries stand out:

> **17:23 UTC:** A former maintainer, André Arko, emails the Director of Open Source at Ruby Central stating that he still has access to the RubyGems.org production environment and associated monitoring tools.  

> **17:30 UTC:** Joel Drapper (unaffiliated with Ruby Central) publishes a [public blog post](https://web.archive.org/web/20250930213611id_/https://joel.drapper.me/p/ruby-central-security-measures/) within minutes describing this access with screenshots taken earlier that day showing root account access.

> **18:20 UTC:** Ruby Central begins its emergency review and learns that the existing credentials for the AWS root account in our password vault are no longer valid.

This is the earliest time that Ruby Central learns something is amiss with their AWS account. However, if you scroll down to their "Analysis of Events" section you'll see a number of events stretching all the way back to September 18. It turns out that this root password change took place over ten days prior on September 19, 2025, without anyone at Ruby Central being any the wiser about it. This is an astonishing admission, most notably because AWS will send an email notification to the root user email address whenever the password is changed. Apparently, nobody at Ruby Central is looking at the emails sent to this address - otherwise, they would have noticed this initial reset on September 19, eleven days before they eventually did. 

They are also extremely fortunate that the threat actor did not end up changing the root account email as well; there seems to be a reason for that, which I'll discuss below. Since this email was not changed, they are able to regain control of the account in the same manner that they lost it:

> **18:24 UTC:** Ruby Central initiates an AWS password-reset procedure, validates multi-factor authentication, and regains control of the AWS root account.

## An Incomplete Post-Mortem

What's even more perplexing is how quickly this post-mortem jumps to to definitively concluding the scope of the incident. Writing under the section "Extent of the Incident":

>After a careful review, Ruby Central is relieved to report **that we see no evidence** that this security incident **compromised end user data, accounts, gems, or infrastructure availability**
> In addition:
>	- RubyGems.org remained fully operational throughout.
>	- No personally identifiable information (PII) of RubyGems.org users nor Ruby Central financial data was accessed or transferred.
>	- The production database, S3 buckets, and CI/CD pipeline were unaffected.

At first glance, this feels like a pretty positive outcome of this event. They reclaimed control of the account and it looks like no irreversible damage occurred. But it's the next section that makes me question just how much we can trust these statements:

>After regaining control of the AWS account, Ruby Central:
>
>1. **Revoked all existing root and IAM credentials**, created new MFA-protected access, and moved them to a restricted vault with per-user audit logs.
>2. **Rotated all related secrets and tokens**, including DataDog, GitHub Actions, and other external system integrations.
>3. **Enabled AWS CloudTrail, GuardDuty, and DataDog alerting** for any root login, password change, or IAM modification.

The third item there is a pretty big red flag. Prior to this incident, they weren't configuring CloudTrail (audit logs), Guard Duty (threat detection), or just basic alerting for the account. Without this context being collected and (ideally) being forwarded to a separate repository outside of AWS that would require separate access to tamper with, it casts a lot of doubt on their earlier conclusions.

As bad as that line sounds, AWS still collects and retains 90 days of CloudTrail logs for your account by default, something that can not be disabled. Since the whole timeline of this incident is a little less than two weeks, that falls well within the retention period for an investigation. 

But (and this is a big but!) the issue is that this default CloudTrail configuration only includes management events. Data events that capture actions like users downloading objects from S3 buckets uploading objects to S3 buckets, API activity on an RDS database cluster, and executing Lambda functions are **not** included in that default configuration. Therefore, it is quite possible that Ruby Central does not have any logs that can conclusively say that the actor did **not** download objects from S3 or touch the production database. Of course, they may know this, which is why their statement is structured to say they "see no evidence" - they don't have any to check. 

I would've also hoped for them to provide a full list of actions the actor took that they can see in the CloudTrail management events to further support their timeline of events - but alas, that was not included either.

## The Other Side of the Story

The plot thickens, however, with a [blog post published](https://andre.arko.net/2025/10/09/the-rubygems-security-incident/) by the alleged actor, André Arko. He acknowledges the rotation of the root user password:

>Given Marty’s claims, the sudden permission deletions made no sense. Worried about the possibility of hacked accounts or some sort of social engineering, I took action as the primary on-call engineer to lock down the AWS account and prevent any actions by possible attackers. I did not change the email addresses on any accounts, leaving them all owned by a team-shared email at rubycentral.org, to ensure the organization retained overall control of the accounts, even if individuals were somehow taking unauthorized actions.

This sequence of actions is pretty interesting for a few reasons. First, if I am the on-call engineer and a security incident is occurring that forces me to change a credential, I am absolutely notifying the other parties that may need that credential that I am rotating it. This is even more important when its something as significant as an AWS account's root credential. In any incident response process, I am also updating the credential with the rotated value in the shared password vault/secrets manager that my team would use. If the rest of the team is asleep or its the weekend, I might send them a note or a Slack message - but as soon as they come back into business hours, I would make sure they acknowledged the change. Instead, André waits for 11 days for any kind of acknowledgement:

>Within a couple of days, Ruby Central made an (unsigned) public statement, and various board members agreed to talk directly to maintainers. At that point, I realized that what I thought might have been a malicious takeover was both legitimate and deliberate

The fact that André waited so long to acknowledge this change in credentials and his prolonged access initially made me have some suspicion about his intention here. However, the fact that he left the root user email address the same (thereby enabling Ruby Central's account recovery days later) shows that maybe his actions were just misguided. And he seems to call out the pretty immature security posture of Ruby Central in general:

>In addition to ignoring the (huge) question of how Ruby Central failed to secure their AWS Root credentials for almost two weeks, and **appearing to only be aware of it because I reported it to them**, their reply also failed to ask whether any other shared credentials might still be valid. There were more.

## Conclusion

All in all, this whole incident and the write-ups that have come out of it do not reflect well on the Ruby community, and would very much shake my confidence in the ability of Ruby Central to be good stewards of RubyGems moving forward. 
Recently, Ruby Central, the non-profit responsible for maintaining the RubyGems package manager, suffered a security incident where they temporarily lost control of their AWS account. They have since [published a post-mortem](https://rubycentral.org/news/rubygems-org-aws-root-access-event-september-2025/) of this event that is ostensibly aimed at putting their community's minds at ease. Unfortunately, it had the opposite effect on me, causing me to come away with more questions than  answers. 
