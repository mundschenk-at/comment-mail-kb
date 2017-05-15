---
title: How can I uninstall Comment Mail but keep my data?
categories: questions
tags: pre-sale-faqs
author: renzms
github-issue: https://github.com/websharks/comment-mail-kb/issues/35
toc-enable: off
---

To delete Comment Mail safely, but retain your custom settings and Subscription data, simply follow the steps below:

- Make sure that **Data Safeguards** in **WordPress Dashboard → Comment Mail → Config. Options → Data Safeguards** is **enabled**
- Locate the Comment Mail plugin in **WordPress Dashboard → Plugins** and choose **Deactivate**
- Locate the Comment Mail plugin in **WordPress Dashboard → Plugins** and choose **Delete**
- Click **Yes, Delete these files and data**

If you leave **Data Safeguards** enabled, deleting the Comment Mail plugin does not erase any of the settings from the WordPress database and when you reinstall Comment Mail, those existing options in the database will be used and your previous configuration will be restored. This also applies to Subscription data—when Data Safeguards are enabled, Comment Mail will keep the Subscription data in the database.

![Comment Mail: Data Safeguards](https://cloud.githubusercontent.com/assets/13220018/23026700/10d1e0d6-f49d-11e6-8781-21efc259f52a.png)

## Import / Export Options

If you're using Comment Mail Pro, you can export your Comment Mail options from **WordPress Dashboard → Comment Mail → Config. Options → Import/Export Options** and then reimport those options later (either after reinstalling Comment Mail or even on another WordPress site).

![Comment Mail: Import/Export Config](https://cloud.githubusercontent.com/assets/13220018/23026680/0001dbda-f49d-11e6-8742-68f988eafee1.png)