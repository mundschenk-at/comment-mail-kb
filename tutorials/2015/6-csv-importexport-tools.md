---
title: CSV Import/Export Tools
categories: tutorials
tags: import-export-tools
author: jaswsinc
github-issue: https://github.com/websharks/comment-mail-kb/issues/6
---

The format required for importation is [CSV (Comma Separated Values)](http://en.wikipedia.org/wiki/Comma-separated_values). The importation routine will accept direct CSV input in a textarea provided by Comment Mail™, or you can choose to upload a prepared CSV file. In either case (direct input or file upload) the first line should be a list of columns you're importing; aka: CSV Headers. CSV Column Headers (like each column value that you provide); should be encapsulated by double quotes. Here is a quick example of how this works.

```text
"post_id", "email", "status"
"1", "john@example.com", "subscribed"
"1", "jane@example.com", "subscribed"
```

_In this example we create two subscriptions. One for `john@example.com` and another for `jane@example.com`. They are both subscribed to all comments/replies on post ID `1` without needing to confirm. The first line is a list of the column we are importing. Each line that follows is a subscription with data matching the column headers (i.e. in the same order as the headers)._

---

## Importing New Subscriptions

### Suggested CSV Column Headers

- `post_id` A WordPress post ID. This field is required. It establishes which post the subscription is for. Every subscription must be associated with a WordPress post.

- `email` Subscriber's email address. This is a required column of course.

- `status` One of the following: `unconfirmed`, `subscribed`, `suspended`, or `trashed`. If you omit this column it will default to `unconfirmed`. To auto-confirm an imported subscriber set this to `subscribed`.

  _If you omit this (or set it explicitly to `unconfirmed`) and you also check the box during import to "Process Confirmation Emails"; then an email confirmation will be sent for each subscription that is marked with an `unconfirmed` status._

### All Possible CSV Column Headers

- `user_id` An association between a comment subscription and a WordPress user ID; if applicable. If you omit this column it will default to a value of `0` automatically; i.e. no association with a WP user.

- `post_id` A WordPress post ID. This field is required. It establishes which post the subscription is for. Every subscription must be associated with a WordPress post.

- `comment_id` A WordPress comment ID; iff the subscription is for a specific comment. If you omit this column it will default to a value of `0`; i.e. no specific comment — which indicates that the subscription will be for all comments/replies on the `post_id`; not to a specific comment.

- `deliver` The delivery option. One of `asap` (for instant notifications), `hourly`, `daily`, `weekly`. If you omit this column it will default to `asap` automatically. Any value that is not `asap` results in a notification that is a digest instead of simple instant notifications.

- `fname` Subscriber's first name. If you omit this column and there is a `user_id` column, the first name will be taken from the user's data within in WordPress (if possible). If all else fails, a first name will be auto-generated based on the portion of the email address that comes before the `@` symbol.

- `lname` Subscriber's last name. This is optional and will simply default to an empty string if you omit this column.

- `email` Subscriber's email address. This is a required column of course.

- `insertion_ip` The IP address the subscriber was using at the time of the subscription. If you omit this column, Comment Mail™ will fill it automatically the first chance it gets to acquire the subscriber's IP address.

- `insertion_region` A two-character geographic location code, which follows the ISO-3166-2 standard. Note that ISO-3166-2 region codes actually consist of 4 characters, but that includes the country code also. Comment Mail™ stores the country code in separate DB column, so this field (while it does follow the ISO-3166-2 standard) should simply contain the region code itself, minus the country code. See: <http://en.wikipedia.org/wiki/ISO_3166-2> for further details. If you omit this column, Comment Mail™ will fill it automatically the first chance it gets to acquire the subscriber's IP address, and thus determine its geographic location.

- `insertion_country` A two-character country code which identifies a geographic location. This column follows the ISO-3166-1 and ISO-3166-2 standards; i.e. a two character country code is all that's needed here. See: <http://en.wikipedia.org/wiki/ISO_3166-1> for further details. If you omit this column, Comment Mail™ will fill it automatically the first chance it gets to acquire the subscriber's IP address, and thus determine its geographic location.

- `last_ip` The subscriber's last known IP address. If you omit this column, Comment Mail™ will fill it automatically the first chance it gets to acquire the subscriber's IP address.

- `last_region` The subscriber's last known geographic region, based on the last known IP address. If you omit this column, Comment Mail™ will fill it automatically the first chance it gets to acquire the subscriber's IP address, and thus determine its geographic location.

- `last_country` The subscriber's last known country code, based on the last known IP address. If you omit this column, Comment Mail™ will fill it automatically the first chance it gets to acquire the subscriber's IP address, and thus determine its geographic location.

- `status` One of the following: `unconfirmed`, `subscribed`, `suspended`, or `trashed`. If you omit this column it will default to `unconfirmed`. To auto-confirm an imported subscriber set this to `subscribed`.

  _If you omit this (or set it explicitly to `unconfirmed`) and you also check the box during import to "Process Confirmation Emails"; then an email confirmation will be sent for each subscription that is marked with an `unconfirmed` status._

---

## Mass Updating Existing Subscriptions

### Suggested CSV Column Headers

- `ID` This indicates that you want to update an existing subscription with this particular ID. If you are updating existing subscriptions this will be a required column.

  _The `ID` column is all that's required for updates. However, you obviously want to provide at least one of the other columns if you intend to actually change something about a particular subscription._

 _When updating existing subscriptions, any column that is simply not given by your CSV file will be left unchanged; i.e. as it exists already for each subscription in your database._

### All Possible CSV Column Headers

- `ID` Subscription database ID used to update an existing subscription instead of creating a new one.

- `key` This column is provided in export files generated by Comment Mail™ and it is accepted when importing, but ignored internally. A subscription `key` is only created and/or updated systematically by Comment Mail™ itself. Thus, while you can provide this column in an import file, Comment Mail™ will ignore it and instead deal with subscription key generation and/or key changes automatically.

  _A subscription key is auto-generated for each subscription when it is created. It is not changed after this, unless and until the `email` is changed to something new. Each time a subscription's email address changes, the key associated with that subscription is also changed by Comment Mail™ automatically._

- `user_id` An association between a comment subscription and a WordPress user ID; if applicable. Use a value of `0` to indicate there is no association with a WP user.

- `post_id` A WordPress post ID. This field is required. This establishes which post the subscription is for. This value must be >= `1`. Every subscription must be associated with a WordPress post.

- `comment_id` A WordPress comment ID; iff the subscription is for a specific comment. Use a value of `0` to indicate no specific comment; i.e. the subscription will be for all comments/replies on the `post_id`; not to a specific comment.

- `deliver` The delivery option. One of `asap` (for instant notifications), `hourly`, `daily`, `weekly`. Any value that is not `asap` results in a notification that is a digest instead of simple instant notifications.

- `fname` Subscriber's first name.

- `lname` Subscriber's last name.

- `email` Subscriber's email address.

- `insertion_ip` The IP address the subscriber was using at the time of the subscription. If this is empty for any subscription, Comment Mail™ will fill it automatically the first chance it gets to acquire the subscriber's IP address.

- `insertion_region` A two-character geographic location code, which follows the ISO-3166-2 standard. Note that ISO-3166-2 region codes actually consist of 4 characters, but that includes the country code also. Comment Mail™ stores the country code in separate DB column, so this field (while it does follow the ISO-3166-2 standard) should simply contain the region code itself, minus the country code. See: <http://en.wikipedia.org/wiki/ISO_3166-2> for further details. If this is empty for any subscription, Comment Mail™ will fill it automatically the first chance it gets to acquire the subscriber's IP address, and thus determine its geographic location.

- `insertion_country` A two-character country code which identifies a geographic location. This column follows the ISO-3166-1 and ISO-3166-2 standards; i.e. a two character country code is all that's needed here. See: <http://en.wikipedia.org/wiki/ISO_3166-1> for further details. If this is empty for any subscription, Comment Mail™ will fill it automatically the first chance it gets to acquire the subscriber's IP address, and thus determine its geographic location.

- `last_ip` The subscriber's last known IP address. If this is empty for any subscription, Comment Mail™ will fill it automatically the first chance it gets to acquire the subscriber's IP address.

- `last_region` The subscriber's last known geographic region, based on the last known IP address. If this is empty for any subscription, Comment Mail™ will fill it automatically the first chance it gets to acquire the subscriber's IP address, and thus determine its geographic location.

- `last_country` The subscriber's last known country code, based on the last known IP address. If this is empty for any subscription, Comment Mail™ will fill it automatically the first chance it gets to acquire the subscriber's IP address, and thus determine its geographic location.

- `status` One of the following: `unconfirmed`, `subscribed`, `suspended`, or `trashed`. To auto-confirm a subscriber set this to `subscribed`.

  _If you set this to `unconfirmed`, and you also check the box during import to "Process Confirmation Emails"; then an email confirmation will be sent for each subscription that is marked with an `unconfirmed` status._

- `insertion_time` A UNIX timestamp (UTC time) indicating the time this subscription took place.

- `last_update_time` A UNIX timestamp (UTC time) indicating the last time this subscription was updated. This field is accepted during import, but if you are updating existing subscriptions the value is automatically defined whenever the update takes place. Making this column simply not necessary during any sort of importation.
