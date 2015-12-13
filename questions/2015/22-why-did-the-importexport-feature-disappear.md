---
title: Why did the Import/Export feature disappear?
categories: questions
tags: import-export-tools
author: raamdev
github-issue:
github-issue: https://github.com/websharks/comment-mail-kb/issues/22
---

The Comment Mail Import/Export feature is a Pro-only feature, however if you're running Comment Mail Lite and your database contains subscription data from certain subscription plugins (such as Subscribe to Comments Reloaded), Comment Mail will show the Import option so that you can import that existing subscription data into Comment Mail.

![2015-12-12_18-59-03](https://cloud.githubusercontent.com/assets/53005/11764634/880ffbfc-a105-11e5-86ad-32bd4e21742d.png)

If you delete the subscription data from your database (which happens when you deactivate and delete  the other plugin, e.g., when you deactivate and delete Subscribe to Comments Reloaded), Comment Mail will no longer detect that subscription data in your database and will therefore hide the Import option (there is nothing in the database for Comment Mail to import, so the option is hidden).