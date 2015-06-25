---
title: StCR Options Transitioned by Comment Mail
categories: tutorials
tags: stcr
author: jaswsinc
github-issue: https://github.com/websharks/comment-mail-kb/issues/11
---

Comment Mail is a highly evolved plugin that is based on the original StCR ([Subscribe to Comments Reloaded](https://wordpress.org/plugins/subscribe-to-comments-reloaded/)) plugin for WordPress. StCR gained enormous popularity in the WordPress community over a span of several years. This new improved version of StCR (now referred to as Comment Mail™) is backward compatible with most features provided by StCR.

If you were previously running StCR, you can upgrade to Comment Mail right away. Many of your existing StCR options are automatically interpreted by Comment Mail whenever you activate it from the WordPress Dashboard. This saves you time and makes the transition much easier.

In addition, if you were previously running StCR, you will be prompted by Comment Mail upon activation. Comment Mail will ask you to begin an import of all of your existing StCR subscribers so that you won't lose any of those important people that establish your fan base.

## Which StCR Options Are Transitioned by Comment Mail?

### Show Subscription Box?

![](https://www.filepicker.io/api/file/svus12vKTJOnWj0A0c4k#.png)

If you had this set to "No" in your StCR options, Comment Mail will automatically disable the same option in its own configuration. In addition, Comment Mail adds backward compatibility for the StCR API Function: `subscribe_reloaded_show()`. If you were using this with StCR, it will continue to work in Comment Mail; i.e., it produces the Comment Mail Subscription Options for you, just like StCR did.

![](https://www.filepicker.io/api/file/jH75qr3ROqa24CFGtI22#.png)

---

### Default Subscription Type

![](https://www.filepicker.io/api/file/YDdUGkqAQqaTE5ctYQJg#.png)

Options in Comment Mail are slightly different, but Comment Mail does its best to match what you had configured in StCR. i.e., All Comments by default, or Replies Only? With Comment Mail you may also tweak the Subscription Options template to adjust the "Checked by Default?" config. option that was available in StCR. Comment Mail templates (simple or advanced) provide a lot of flexibility.

![](https://www.filepicker.io/api/file/T5LS5xnsRWmxJuAfxt0E#.png)

---

### "Track all subscriptions?" or "Bcc Admin on Notifications?"

![](https://www.filepicker.io/api/file/oZ0rGMKYRyK5vUUA50Et#.png)

If either of these were checked in your StCR config. options, Comment Mail will automatically Auto-Subscribe the site Administrator whenever a new post is published. This is not fully compatible with StCR, because Comment Mail doesn't Bcc anyone, ever. However, a similar behavior is accomplished by automatically adding the site Administrator's email to the list of Auto-Subscribe recipients.

![](https://www.filepicker.io/api/file/IXlRyK4GSaWpNAGybc2r#.png)

---

### Other StCR Options Transitioned by Comment Mail

- The `From:` name and email address header you had configured with StCR.
- The "Enable Double Check?" option in StCR is picked up by Comment Mail; i.e., automatically confirm, or require email confirmation?
- The "Subscribe Authors?" option in StCR is picked up by Comment Mail; i.e., will enable or disable post authors in Comment Mail's Auto-Subscribe functionality.

---

## What's Left For Me To Review?

### Basic Config. Options in Comment Mail

See: **Dashboard → Comment Mail → Config. Options**

_You should review each of these options, and be sure to enable Comment Mail :-)_

![](https://www.filepicker.io/api/file/6PsVJVXLTpSmNNT5iK0f#.png)

---

#### CAN-SPAM Compliance Options

- Please see: **Dashboard → Comment Mail → Config. Options → CAN-SPAM Compliance**
- See also: [Understanding CAN-SPAM Compliance in Comment Mail](http://comment-mail.com/kb-article/can-spam-compliance/)

---

### Subscribers! — Comment Mail Can Import Subscribers Too

- Please see: **Dashboard → Comment Mail → Config. Options → Import/Export → StCR Import**

![](https://www.filepicker.io/api/file/XVbcGkGHTBWXX0djoxYf#.png)