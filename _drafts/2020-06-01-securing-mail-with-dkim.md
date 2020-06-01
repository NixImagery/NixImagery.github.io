---
layout: post
title: Securing mail using DKIM
# date: 2019-11-26 20:10
# description: 
img: R0000416.jpg
fig-caption: Durham
fig-attrib: Nick Hood
published: yes
tags:
- Plesk
- DNS

# permalink:
---
Over the weekend, as I was updating DNS tables for a client, I thought I'd sharpen up my server mail settings to make the mail service more robust. I've seen (unrelated to this) an increase in spam recently and it had been on my mind to do more to combat it. These notes set out broadly how I configure my mail server.

## Mail server settings
The mail server I use is Postfix/Dovecot. Using the Plesk control interface on my VPS[^vps], there are a number of settings needed to mitigate the scourge that is spam emails. From Tools & Settings, select Server-wide mail settings make these changes.

### Using DNS Blacklisting
The first thing to do is to switch on spam protection based on DNS blackhole lists such as [zen.spamhaus.org](https://www.spamhaus.org/), [spam.abuse.ch](https://abuse.ch/) and [spamrbl.imp.ch](https://imp.ch/). Also, when you do get spam in your inbox, report it immediately. This means just copying the message source[^notthat] into a form at somewhere like [SpamCop.net](https://www.spamcop.net/), who will send abuse reports to the ISPs that allow the spammers access to the internet. What we hope is that these providers will shut them down, but some are repeat offenders: all of my recent reports have gone to [CloudFlare](https://www.cloudflare.com/) who seem reluctant to combat internet abuse, perhaps because they are making money out of it.

## SPF
[Sender Policy Framework](http://www.faqs.org/rfcs/rfc7208.html) is designed to allow domain admins to authorize the hosts that are allowed to use their domain names. Receiving mail servers can check that authorisation by looking up the SPF record of the domain claimed in the "from" field of an email.

Under `SPF spam protection`, check `Enable SPF spam protection to check incoming mail` and select `Only create Received-SPF headers, never block` from the drop-down.

Your own domains should also have an SPF code in the DNS table. This acts like a return address on a snail-mail envelope. Servers can check the sender's IP against this DNS record to check that it is allowed to send mail on behalf of the domain. This record identifies the version of SPF being used (always 1 at the moment), which records pertain and what policy should be applied to mail that fails the check when this record is checked by the receiving mail server. `-a` is a hard fail setting which advises rejection of mail that doesn't match the record parameters. `~a` is a soft fail, and `+a` is like leaving your keys in the front door.

## DKIM


## DMARC
Bringing the measures together, with a DNS-based reporting mechanism that closes the loop, is DMARC. This helps protect the domain from unauthorized use. It also requires a DNS TXT entry which identifies policy for handling non-aligned (mail that looks like it might be spam) emails, and a place to send reports about tases incidents. Setting up needs the policy to be passive, or "reporting only", set by `p-none` in the DNS record. Increasing levels of confidence in the deliverability of email from the server allows organisations to increase this policy to "quarantine", or even "reject". Email reports are sent for authentication failure (forensic) and summary information (aggregate) to the email addresses in the record.

## Summary
The final DNS aligns with the server settings to provide a more robust and spam-free[^orly] mail experience.

An example DNS set of mail-related TXT entries:

Host name|Record type|Address
:--------|:----------|:------
@|TXT|v=spf1 +a +mx -all
_domainkey|TXT|o=-
default._domainkey|TXT|v=DKIM1;k=rsa; p=yourkeygoeshere
_dmarc|TXT|v=DMARC1; p=none; rua=mailto:aggregate@yourdomain.tld; ruf=mailto:forensics@yourdomain.tld; fo=1

## Notes

[^orly]: Well, we will see how it goes.

[^notthat]: Not the body of the email. The DNS blacklisters need to see the contents of the email header, which reveals where it came from and how it was routed to your computer. Filter scores are also included here. On a mac, if you're using Mail.app, just click in the body of the mail message and click cmd-alt-u to get a pop-up with the email message source. Cmd-a, cmd-c, and then paste it in the textbox on the spamcop form.

[^vps]: Virtual private server. Literally, a Dell server, in a rack, connected to the T1 backbone in London. Mine runs Centos, a variant of RedHat specifically designed for this kind of job. My ISP for the past 20 years has been [Hosting UK](https://hostinguk.net/), run by Phil Parry, who set the business up in his garage. It's now part of the Scottish IT business [IoMart](https://www.iomart.com/).