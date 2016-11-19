---
title: Replies via Email: SparkPost or Mandrill?
categories: questions
tags: rve
author: raamdev
github-issue:
github-issue: https://github.com/websharks/comment-mail-kb/issues/28
---

Comment Mail supports both SparkPost and Mandrill for the Replies via Email integration. If you're trying to decide which service to use, here are several important differences to consider:

- SparkPost is free and easier to setup and configure.
- However, SparkPost does not support the additional spam score setting in Comment Mail like Mandrill does; i.e., the SparkPost API does not provide Comment Mail with a spam score in the API response like Mandrill does.
- Also, SparkPost does not support the additional SPF spam check in Comment Mail like Mandrill does; i.e., the SparkPost API does not provide Comment Mail with an SPF test result in the API response like Mandrill does.
- Also, SparkPost does not support the additional DKIM spam check in Comment Mail like Mandrill does; i.e., the SparkPost API does not provide Comment Mail with a DKIM test result in the API response like Mandrill does.

If you're looking for better spam protection, Mandrill has better options for that but it comes with an added cost. SparkPost, on the other hand, is free and easier to set up.

----

See also:

- [SparkPost RVE Handler](http://comment-mail.com/kb-article/sparkpost-rve-handler/)
- [Mandrill RVE Handler](http://comment-mail.com/kb-article/mandrill-rve-handler/)