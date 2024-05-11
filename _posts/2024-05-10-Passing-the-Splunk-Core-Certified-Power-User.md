---
title: How to Pass the Splunk Core Certified Power User
date: 2024-05-10 00:22:47 -1000
categories: [Certifications, Splunk]
tags: [certifications, Splunk]
---

An important tool in the arsenal of a cybersecurity analyst is a Security Information and Event Management (SIEM) solution, which aggregates, correlates, and stores security logs, events, and messages in real-time. One of the most popular SIEMs in corporate environments is Splunk, which uses forwarders, indexers, and search heads to forward, ingest, parse, store, and search raw network data and events. As part of its certification program, Splunk offers the Splunk Core Certified Power User, which validates a user's ability to use Search Processing Language (SPL) efficiently, create knowledge objects and dashboards, and normalize data using datasets and the Splunk Common Information Model (CIM). This was a very fun certification to achieve, and this article will go over my thoughts.

## Overall Thoughts

As already mentioned, this was a very fun certification to achieve. The learning curve is not as steep as Splunk's higher-level certifications, but learning how to use SPL, create knowledge objects, and and use datasets gave enough of a challenge for someone who barely knew how to search an index efficiently. After achieving this certification, I have already built two search macros that exponentially speed up the investigation process of Cloudflare and Netskope logs. They are not perfect, but they are much better than the default SPL searches that the SOC uses regularly.

**Cloudflare_Search(2)**
> index=cloudflare source="cloudflare-firewall" Action!=block ClientIP=*$IP_Address$* ClientRequestUserAgent="*$UserAgent$*"
> | search NOT status IN (403 400 404 499) NOT ClientASN IN (13485 55256) NOT Description IN ("Terraform Rule - Allow Access to Admin Ajax" "Terraform Rule - Allow from internal IPs" "Allow from Internal IPs")
> | eval URL = ClientRequestHost+""+ClientRequestPath, Time = strftime(_time, "%a %m-%d-%Y %H:%M:%S"), Referer = if(Referer = "", null(), Referer)
> | table Time, ClientIP, ClientCountry, ClientASN, ClientRequestUserAgent, ClientRequestMethod, ClientRequestReferer, URL, status
> | rename ClientIP as "IP Address", ClientCountry as "Origin Country", ClientASN as "ASN", ClientRequestUserAgent as "User Agent", ClientRequestMethod as "HTTP Method", ClientRequestReferer as "Referer", status as "HTTP Response Status Code"
> | fillnull value="N/A"

**Netskope_Search(3)**
> index=netskope user=*$user$*
> | search url=*$url$* OR referer=*$url$*
> | search hostname=*$ComputerName$*
> | eval Browser = browser+" "+browser_version, Referer = if(referer = "", null(), referer), app = if (app = "", null(), app)
> | table src_time, src_timezone, userip, dstip, hostname, user, os, Browser, referer, url, app, activity, action
> | rename src_time as "Time", src_timezone as "Timezone", userip as "GCU IP Address", dstip as "Website IP Address", hostname as "Computer Name", user as "User", os as "Operating System", referer as "Referer", url as "URL", app as "App", activity as "Activity", action as "Action Taken"
> | fillnull value="N/A"

## General Tips and Tricks

The Splunk Core Certified Power User already assumes you have Splunk Core Certified User knowledge, so it skips over the components of Splunk and the basics of SPL and dashboards. As a result, you will either need to go back and obtain the Splunk Core Certified User certification first or go through its content before attempting the Splunk Core Certified Power User exam.
- Any command, command modifier, function, and argument covered in both the Splunk Core Certified user and Core Certified Power User exams is fair game, so go through the exam blueprints of both exams and go through the Splunk documentation thoroughly.
- **This exam requires hands-on practice with SPL commands.** Boot up an Ubuntu Server VM, install Splunk Enterprise, cretae an index, set up a listener on tcp/9997, boot up a Windows 10 workstation VM, install the Splunk Universal Forwarder, and forward any event log such as Windows Defender logs to Splunk Enterprise. You *will* have to go through a lot of documentation, forum posts, and online articles to learn how to do this, but the knowledge gained is invaluable.
- This exam will try to catch you on every single small detail. Read the answer choices carefully and see which answer actually answers the question and produces the visualization shown on screen.

## Recommended Training Materials

I highly recommend Hailie Shaw's [Splunk: Zero to Power User](https://www.udemy.com/course/splunk-zero-to-power-user/) video course on Udemy. She is personable and charismatic with her teaching, and she covers most of what you need to know for the exam in layman's terms. I also highly recommend that you go through [Splunk SPL2 documentation](https://docs.splunk.com/Documentation/SCS/current/SearchReference/Introduction) for every command, command modifier, function, and argument she shows and demonstrates.

## Conclusion

Learning how to execute searches in a SIEM is an invaluable skill for any cybersecurity analyst, and because most SIEMs use very similar search languages, knowing how to craft powerful SPL searches can be a very powerful skill to learn, regardless of which SIEM a company uses. If you have any questions about the Splunk Core Certified Power User certification, feel free to DM me on Discord or connect with me on LinkedIn.

## Changelog

**05/10/2024:** Added a changelog.
