---
title: SparkPost RVE Handler
categories: tutorials
tags: rve
author: raamdev
github-issue:
github-issue: https://github.com/websharks/comment-mail-kb/issues/27
---

## What is an RVE Handler?

RVE (**Replies via Email**). An RVE Handler is an integration between Comment Mail and another third-party service, such as [SparkPost](http://comment-mail.com/r/sparkpost/). SparkPost becomes your RVE Handler, but the entire process is not completed until it reaches a final integration that is powered by Comment Mail. Where Comment Mail is a WP plugin that you've installed on your site, which receives and processes replies.

When someone replies to an email notification sent by Comment Mail, the email first goes to SparkPost, and is then routed back to your installation of WordPress, where Comment Mail receives a Webhook data transmission and processes it accordingly. This makes it possible for Comment Mail to process email replies and convert them into comments in a very reliable way.

## Steps Required

This feature is intended for intermediate to advanced site owners; i.e., it's not super-simple, but if you follow these instructions it's not difficult either. Your visitors will thank you for the time you spend here :-) Particularly those who use mobile devices; i.e., replying via email is so much easier.

---

### 1. Get a SparkPost Account ~ Free!

SparkPost does many things but two features, Relay Webhooks and Inbound Domains, make the Comment Mail Replies via Email feature possible. These features happen to be free, so all you need at the moment is to create a free SparkPost account, and create an API key with the Relay Webhooks and Inbound Domains features enabled; you don't need worry about the rest for now. You can signup for a free account here: https://app.sparkpost.com/sign-up

----

### 2. Enable RVE in Comment Mail

Visit **Dashboard → Comment Mail → Config. Options → Replies via Email (RVE Handler)**, enable Replies via Email, and choose SparkPost as your RVE Handler.

  ![Comment Mail - Replies via Email](https://cloud.githubusercontent.com/assets/1563559/20019109/92ce44be-a27f-11e6-811f-08dbecbafba5.png)

---

### 3. Create and configure SparkPost API Key

Login to your SparkPost account and visit the [Account → API Keys](https://app.sparkpost.com/account/credentials) section of your SparkPost account and create a new API Key with permission to read/write to **Relay Webhooks** and **Inbound Domains**. You will then copy and paste the new API Key into your Comment Mail configuration.

  ![SparkPost - Create API Key](https://cloud.githubusercontent.com/assets/1563559/20018808/2d850c4c-a27e-11e6-8279-b237d80bc9f1.png)

  ![SparkPost - Copy API Key](https://cloud.githubusercontent.com/assets/1563559/20019262/37d70180-a280-11e6-987f-a305a5440b21.png)

  ![Comment Mail - Add SparkPost API Key to Comment Mail Replies via Email](https://cloud.githubusercontent.com/assets/1563559/20019168/d145304a-a27f-11e6-8674-199398e4b22a.png)

---

### 3. Creating MX Records

MX records are for email routing and you will need to create a new MX record on your domain to complete the SparkPost integration. Creating an MX record makes it possible to send emails to something like `rve@spark.yoursite.com` and have that email routed to SparkPost's servers. 

We suggest using `spark.yoursite.com` (where `yoursite.com` is your actual domain). Note that this new MX record is NOT for your Outbound Domain or Bounce Domain. It's for a new Inbound Domain that will be dedicated to Comment Mail RVE handling.

  MX record: `spark.yoursite.com MX rx1.sparkpostmail.com 10` 

See also: [SparkPost Inbound Domains documentation](https://developers.sparkpost.com/api/inbound-domains.html)

  _**Warning:** Do NOT use `sparkpost.yoursite.com`; `sparkpost` is a reserved word. Instead use `spark`, which is shorter, sweeter, and not a reserved word in the SparkPost API._

_**Note:** It is best to use a subdomain that is specifically for SparkPost, so as to avoid any interruptions with your existing domain. In the end, this domain is only used for `Reply-To` headers anyway, so it really doesn't need to look pretty; it just needs to work :-)_

#### Getting help creating MX records

If you're not sure how to change MX records given your current registrar or hosting provider, you might take a quick peek at the list that has been compiled by Google. See: https://support.google.com/a/topic/1611273 

Obviously, the instructions provided by Google are for Google MX records, but if you're totally lost, finding your current registrar or hosting provider in this list and going by example should help. Instead of using Google MX records, just follow the instructions and then use the MX record described above for SparkPost (replace `yoursite.com` with your actual domain).

[![Google - Set up MX Records](https://cloud.githubusercontent.com/assets/1563559/5089253/b0be5b04-6ee6-11e4-9321-b78879b73cb5.png)](https://support.google.com/a/topic/1611273)

---

### 4. Configure Comment Mail with an RVE 'Reply-To' address

The 'Reply-To' address should have a domain matching your new MX record, and it should start with `rve@`. Example: `rve@spark.yoursite.com`

  ![Comment Mail - Configure RVE 'Reply-To' address](https://cloud.githubusercontent.com/assets/1563559/20019196/ee4cebd8-a27f-11e6-90fe-0f4964c26dc0.png)

----

See also:

- [Replies via Email: SparkPost or Mandrill?](https://github.com/websharks/comment-mail-kb/issues/28)