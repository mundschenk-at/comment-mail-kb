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

SparkPost does many things, but two features: Relay Webhooks and Inbound Domains, make the Comment Mail Replies via Email feature possible. These features happen to be free, so all you need at the moment is to create a free SparkPost account, and create an API key with the Relay Webhooks and Inbound Domains features enabled; you don't need worry about the rest for now. You can signup for a free account here: https://app.sparkpost.com/sign-up

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

### Replies via Email are Now Enabled ~ Congrats!

---

## When an RVE Handler is Enabled

- Comment Mail™ will allow replies to comments via email using a special `Reply-To` address that you will need to set up by following the instructions provided in this article. Any other Reply-To address configured elsewhere in Comment Mail will be overridden by the address you configure for an RVE Handler. There are no special exceptions to this. An RVE Handler takes precedence over any other `Reply-To` you configure.

- Replies to comments via email will be functional for all types of notifications sent by Comment Mail (including digest notifications). However, there are a few things worth noting before you enable an RVE Handler.

  - All replies posted via email must be sent to the special `Reply-To` address that you configure. Once you configure a `Reply-To` for an RVE Handler, Comment Mail will automatically set the `Reply-To:` header in all email notifications that it sends. This way when somebody replies to a comment notification, their email program will reply to the address required for replies via email to work properly.

  - The `Reply-To` address that you configure, will serve as a base for Comment Mail to work from. For instance, let's say you choose: `rve@spark.yoursite.com`. This base address will be suffixed automatically (at runtime) with details specific to a particular notification that Comment Mail sends. Ultimately, `rve@spark.yoursite.com` will look like: `rve+332-96-kgjdgxr4ldqpdrgjdgxr@spark.yoursite.com`.

    _In this example, the additional details (following the `+` sign) are there to help Comment Mail route the reply to the proper location, and to provide a means by which to identify the end-user that is posting a reply._

  - For single-comment notifications; i.e. where a subscriber chooses delivery type `asap` (aka: instantly), there is just a single comment in each notification that a subscriber receives. This works best with replies via email, since the `Reply-To:` header (on its own) is enough for everything to work as expected. Someone replying via email need only hit the Reply button in their email program and start typing. Very simple.

  - For multi-comment notifications; i.e. where a subscriber chooses a delivery type that is not `asap` (e.g. `hourly`, `daily`, etc.); there can be more than a single comment in each notification they receive. If there is more than one comment in the notification, instructions will be provided to the end-user explaining how to reply. The special `Reply-To` address is still used in this case. However, they also need to specify which comment they want to reply to. To do this, the end-user must start their reply with a special marker provided by Comment Mail. Again, if there is more than one comment in the notification, instructions will be provided to the end-user explaining how to reply.

  - Comments posted via email are still piped through the same underlying WordPress handler that normal on-site comments go through (i.e. `/wp-comments-post.php`). This means that all of your existing WordPress Discussion Settings (and/or Akismet settings) will still apply to all comments, even if they are posted via email.

    **With one exception.** When an RVE Handler is enabled, any comments posted via email are allowed through without an end-user being logged-in. If your WordPress Discussion Settings require that users be logged-in to post comments, that will be overridden temporarily whenever a reply via email comes through.

    Please note that replies posted via email are generally from confirmed subscribers. Any reply via email that is not from a confirmed subscriber will be forced into moderation by Comment Mail anyway. Otherwise, whatever your current Discussion Settings are configured to allow, will be adhered to for replies via email also.

    For instance, if you require that all comments be moderated, that will continue to be the case for all replies via email. Comment Mail will never approve a comment on it's own. Approval of comments is always determined by your WP Discussion Settings.

  - Any reply via email should include one of two things. A copy of the original quoted notification, or a special `!END` marker. Most email clients will include the original message in an email reply, and this is what Comment Mail will look for. Comment Mail scans the body of the email looking for an original quoted section and strips it out (along with anything below it). If a reply does not include a quoted section when replying to an email notification, an `!END` marker can be used instead.

    When Comment Mail reads `!END`, it will use it as a marker and ignore everything below that line. Everything above `!END` will become the comment reply on your blog. Therefore, you can use the `!END` feature even if you have quoting turned off in your email client.

    If neither of these are found, the reply is still accepted. However, it will be forced into moderation at all times; i.e. you must approve it manually no matter what the rest of your WordPress Discussion Settings say.


----

See also:

- [Replies via Email: SparkPost or Mandrill?](https://github.com/websharks/comment-mail-kb/issues/28)
