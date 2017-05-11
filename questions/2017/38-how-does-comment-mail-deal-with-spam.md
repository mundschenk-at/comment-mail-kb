---
title: How does Comment Mail deal with spam?
categories: questions
tags: pre-sale-faqs
author: renzms
github-issue: https://github.com/websharks/comment-mail-kb/issues/38
---

Spam bots surf the Internet every minute of every day—just looking for ways to create free accounts and/or spoof their identity. If you open up your site to commenting and Free Registration (of any sort), you can expect to find lots of this unless you take the proper precautions. Comment Mail provides several tools to help you avoid spam.

You can filter out fake subscriptions by having them first confirm via a valid email. Please see: **WordPress Dashboard → Comment Mail → Config. Options → Auto-Confirm Settings**

![Comment Mail: Auto-Confirm Settings](https://cloud.githubusercontent.com/assets/13220018/23030649/515ac1ca-f4a9-11e6-8914-c38c973ef753.png)

This can be taken a step further by Blacklisting specific email addresses or email patterns. Adding to this list of emails will prevent that email from subscribing to your site. Please see: **WordPress Dashboard → Comment Mail → Config. Options → Blacklisted Email Addresses**

![Comment Mail: Blacklisted Email Addresses](https://cloud.githubusercontent.com/assets/13220018/23030650/515dc8c0-f4a9-11e6-9a86-6cf9e2dcf484.png)

You can also strengthen your settings in WordPress to filter out some spam from anonymous and fake user comments. Please see: **WordPress Dashboard → Settings → Discussion**
 
- Check "Comment author must fill out name and email"
- Check "Users must be registered and logged in to comment"

If you want a more hands on approach to filtering out users and spam, please see the following settings in **WordPress Dashboard → Settings → Discussion**.

![WordPress: Discussion Settings](https://cloud.githubusercontent.com/assets/13220018/23030771/b73eb9d8-f4a9-11e6-9e42-6c5d914926a6.png)

In addition to the Comment Mail tools and the built-in WordPress discussion settings that help avoid spam, you can also integrate Google's reCAPTCHA service into your comment areas by downloading one of the many reCAPTCHA WordPress plugins available. reCAPTCHA is a free service to protect your website from spam and abuse. reCAPTCHA uses an advanced risk analysis engine and adaptive CAPTCHAs to keep automated software from engaging in abusive activities on your site. It does this while letting your valid users pass through with ease.