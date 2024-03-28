---
categories:
- Cloud Security
date: "2024-03-28T00:00:00Z"
description: An update on AWS enabling account-level defaults for the Instance Metadata Service.   
img_path: /assets/img/posts/20240328
pin: false
tags:
- AWS
title: An Easier Way to Enable IMDS Defaults Across All Regions
showTableOfContents: true
---

## Introduction
EC2 instances in AWS can have access to something called the instance metadata service, which makes information (namely *metadata*) about an instance available to applications, services, code, etc. that runs on the instance. For example, a piece of code can query the metadata service to learn what region it is currently running in. 

When an EC2 instance is assigned an instance profile that grants it permissions to access other AWS services, the temporary credentials for that instance profile can also be retrieved from the instance metadata service. This setup is extremely useful, as it allows your code to make authenticated calls to AWS APIs without having to use hardcoded credentials, environment variables, or frequent calls to some off-host credential manager. 

However, the initial version of the Instance Metadata Service (IMDSv1) had a few issues that opened the door for Server Side Request Forgery attacks against applications running on an EC2 instance to steal AWS credentials from IMDS and use them to take action elsewhere in an account. This flaw was the cause of the [Capital One breach back in 2019](https://krebsonsecurity.com/2019/07/capital-one-data-theft-impacts-106m-people/) as well as a number of other security incidents across the industry. 

Since then, AWS made [several improvements in a second version](https://aws.amazon.com/blogs/security/defense-in-depth-open-firewalls-reverse-proxies-ssrf-vulnerabilities-ec2-instance-metadata-service/) of IMDS called, obviously, IMDSv2. However, this setting was not turned on by default for fear of breaking compatibility with existing workloads. Users can opt into this newer version of IMDS when launching new instances, putting the onus on security teams to put up guard rails to ensure that teams were moving to IMDSv2 and burning down the existing use of IMDSv1. 

## A New Default

Back in November 2023, [AWS announced](https://aws.amazon.com/blogs/aws/amazon-ec2-instance-metadata-service-imdsv2-by-default/) that by mid 2024, all EC2 instance types will only use IMDSv2. At the same time, they made it so that all quick launches through the AWS console would only use IMDSv2. These were welcome changes, but did not provide additional tools to allow admins to begin enforcing defaults before the mid-2024 date. 

All of that changed this past week, as [AWS finally rolled out the ability to set defaults](https://aws.amazon.com/about-aws/whats-new/2024/03/set-imdsv2-default-new-instance-launches/) for the Instance Metadata Service at the account level. However, these settings are specific to a single region, meaning that if your account(s) use a large number of regions, you would have to go region by region (through either the CLI or console) to change these settings. 

That inspired me to throw together a very, very quick Python script that aims to first look at the active regions in an account and then cycle through each region and set these new defaults in an automated fashion. It aims to be the least disruptive to existing workflows by only changing the IMDS required version and hop limit, leaving the default setting for enabling IMDS and the ability to pass tags to it alone, unless otherwise specified. You can find this script [here](https://github.com/misczak/aws-imds-defaults). 

While this script is scoped to a single account, if you administer multiple accounts, you can combine this with tools such as [aws-sso-util](https://github.com/benkehoe/aws-sso-util) and [aws-vault](https://github.com/99designs/aws-vault) to quickly change this setting across your entire fleet. 

I hope this helps others speed up the rollout of IMDSv2 defaults across their organization and allows us to collectively put this issue to bed by the end of 2024. 