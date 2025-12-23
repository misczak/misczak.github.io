---
categories:
- Cloud Security
date: "2023-08-18T00:00:00Z"
description: My experience preparing for and passing the GCP Professional Cloud Security Engineer exam.   
img_path: /assets/img/posts/20230818
pin: false
tags:
- GCP
title: Google's Professional Cloud Security Engineer Certification
url: posts/googles-professional-cloud-security-engineer-certification
showTableOfContents: true
---

## Introduction
Earlier this year, my team was provided access to a training budget for Google Cloud Platform that we could use in various ways to purchase classroom trainings or licenses to Google's on-demand training platform, Cloud Skills Boost as well as a number of exam vouchers that could be used on various GCP certification exams. While I had previously worked almost exclusively with AWS (only using GCP for some testing of private service connect), I knew that I had some upcoming projects that required me to build services on GCP. For that reason, I jumped at the opportunity to take advantage of this training and hopefully prepare myself enough to write an exam at the end of it. 

Unbeknownst to me at the time, Google was also offering us a number of seats in what they call their Certification Journey. This program is essentially a focused, six week schedule to work through the Cloud Skills Boost content for your selected certification, with a few extra bonuses layered in. After doing some of the introductory Cloud Skills Boost content and building on GCP myself for a few months, I decided to enroll in the Certification Journey for the Professional Cloud Security Engineer certification. My cohort was scheduled to start in the middle of May, wrapping up by the end of June. 


## Preparing for the Exam

The Certification Journey was an interesting program that lays somewhere between formal classroom SANS training an the open free-for-all that is regular Udemy courses with Discords attached. First, you don't undertake the program alone; you are scheduled into a cohort with others who are aiming for the same certification at that time, and have opted into the program themselves. There's a Google Group set up for discussion among members of the cohort on topics covered in the program, although mine was pretty sparsely used. 

The other interesting wrinkle to the Certification Journey program is that your cohort is assigned an instructor, who holds group "office hours" once a week for 90 minutes to go over that week's content, walk you through sample questions similar to those found on the exam, and most importantly explain to you why the correct answer is the right answer. I was skeptical of these sessions initially, but soon came to find them incredibly valuable. Our instructor pointed out pitfalls I had missed when reading documentation or playing around in GCP myself - such as the fact that BigQuery has its data access logs enabled by default, the only service in GCP to do so. 

The Cloud Skills Boost content is, for the most part, of a very high quality. This content is accessible [outside the Certification Journey program](https://www.cloudskillsboost.google/subscriptions) with just a regular license that runs $29 per month or $300 per year. There are some lectures in there that are less interesting than others, but they're usually kept to byte-sized videos (4-7 minutes in length) that make it easy to fit in between other tasks or meetings in your day. The real value of Cloud Slills Boost, however, are the labs, as they spin up an ephemeral project for you to create resources and mess around in. Once the lab is complete, they tear down the project and any resources within. It's great for peace of mind, as you don't have to worry about making sure you disposed of every resource you used in a lab that could end up billing you. 

In addition to all this content, each week there was a series of links to documentation, blog posts, and videos for further reading and watching. I held off on watching these until I got through most of the Cloud Skills Boost content, knowing that each one would be part of a deeper dive into a service or feature. In the last week or so before my exam, I was working through these links non-stop and watching any video I could find on each service. There are some services I would probably never get the chance to play around with hands on (like setting up Cloud Interconnect for the first time), but I felt prepared for everything else.

Interestingly, I didn't feel the need to do a practice exam, as the sample questions from the instructor office hours gave me a good preview of what the questions from the exam itself would be like. These sample questions were scenario based, with each possible answer often being a series of steps and actions you would take in GCP - not just simple recall of a service's name or feature. The questions also leaned away from any "gotchas" where the right answer is surrounded by wrong answers that are just spelled differently, or something similar. This setup made me feel confident that I wouldn't have to memorize the exact form of every IAM predefined role or setting, as just knowing  what role types would have what permissions would suffice. 

## Sitting the Exam
I've done a couple of certification exams before, and the registration and check-in process was pretty similar to those. The exam itself was 45 questions, and I flew through the first ten questions before finding the next thirty-five much more detailed and challenging. However, I didn't have any questions where I was completely at a loss to answer - instead, if I wasn't 100% sure of my answer, I marked it for review and moved on. At the end of my first pass of the exam, I had about nineteen questions marked for review and did another loop through those, which whittled it down to nine questions I still was 50/50 on between two answers. I spent some additional time on those and then submitted my exam. Total time was about one hour, ten minutes. 

## Results
The test results screen immediately showed that I had achieved a provisional pass, but would have to wait for an email from Google Cloud for confirmation. This took about a day and a half to arrive, with links to setup a profile for my badge on Accredible. There was also a token to use in the swag store for those who passed Professional tier GCP exams, which allowed me to have a certification welcome kit to be mailed to me. I've heard in years past this used to be a hoodie or something similar, but the only option on the store available to me was the thermal mug seen in the picture below.

[![The GCP certification welcome kit I received](images/gcpwelcomekit.png)](images/gcpwelcomekit.png)

All in all, I would say my experience of preparing for and achieving this certification was a positive one. The material did not feel endless, instead really focusing in on the best ways to set up secure organizations and projects in GCP. I came to appreciate the format of the questions, which avoided focusing on what I would call trivia and instead emphasizing really understanding the sequence of steps and nuance needed for good security. 