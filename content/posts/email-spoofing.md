+++
title = 'Email spoofing'
date = 2024-05-16T16:24:05-07:00
+++

It's possible to send emails "from" any email address, even ones that don't belong to you.

> **Email spoofing** is the creation of email messages with a forged sender address.
> 
> — [Email spoofing - Wikipedia](https://en.wikipedia.org/wiki/Email_spoofing#:~:text=email%20spoofing%20is%20the%20creation%20of%20email%20messages%20with%20a%20forged%20sender%20address.)

Spammers and phishers sometimes do this to trick people. Unfortunately, it's impossible to prevent. This can happen even if your account is not compromised.

One of my email addresses was spoofed in at least one email. However, one of the recipient addresses did not exist, so I received a bounce message from Google. That's how I found out my address was spoofed.

Here's the bounce message:

![spoofed email bounce message](/spoofed-email-bounce-message.png)

I didn't check the attachment. The URL of the "LEARN MORE" link is legitimate: https://support.google.com/mail/?p=NoSuchUser

In this case, [Google recommends](https://support.google.com/mail/answer/50200?hl=en&sjid=11313421216828233515-NC) marking the bounce message as spam.
