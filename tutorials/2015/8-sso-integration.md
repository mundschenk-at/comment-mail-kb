---
title: SSO Integration
categories: tutorials
tags: sso
author: jaswsinc
github-issue: https://github.com/websharks/comment-mail-kb/issues/8
---

As a convenience, SSO (Single Sign-on) allows commenters (or any user for that matter) to login with a popular social network account; e.g. Twitter, Facebook, Google, LinkedIn. This feature is highly recommended, but disabled by default; since it requires some work on your part to set things up properly. No worries though, we will walk you through the entire process in this article.

## In a hurry? Jump to:

- [Twitter](#-twitter)
- [Facebook](#-facebook)
- [Google](#-google)
- [LinkedIn](#-linkedin)

## Overview of Single Sign-on (SSO)

When a visitor logs in through an SSO service provider, an account is automatically created for them in WordPress (if one does not exist already). These auto-generated WordPress accounts are created using details obtained from an SSO service provider. Such as first name, last name, email address. SSO users receive a default Role; i.e. whatever the default Role is for your site. Normally the [Subscriber Role](http://codex.wordpress.org/Roles_and_Capabilities#Subscriber), but you can change this from your WP General Settings on standard WP installs. WP Multisite Network installs always use the Subscriber Role.

An account created in this way (via SSO) could be logged into like any other WP account (technically), but it will also be connected to the underlying SSO service too. Meaning, a user may simply log into your site in the future w/ the SSO. They won't ever need a username/password that is specific to your site.

### If somebody logs in with Twitter, Facebook, Google, LinkedIn, etc.; are they associated with a username/password on my site too? If so, how would they log in with those credentials?

When somebody logs in via Twitter, Facebook, Google, LinkedIn, etc.; there is no need to ask the user for a username/password. Authentication occurs through the SSO provider, so this is not necessary. That said, the answer to this question is yes. There is also a generic username/password that is site-specific, which sits quietly behind-the-scenes. It serves no useful purpose though, unless you come up with one on your own.

To clarify, when Comment Mail™ auto-generates a WP account for them, they _will_ be assigned a generic username/password that they could log in with via `/wp-login.php` if you wanted them to. Auto-generated usernames/passwords are not very friendly though, and they are not given to the user; as this is not necessary. However, if you choose to look-up their account in your Dashboard (search by name or email address), you could obtain the generic username and reset their generic password yourself; for the purpose of relaying that information to an end-user that wants it. But, again, this is not necessary. The end-user can just continue to log into your site with the SSO service they originally created their account with. They have a generic username/password that is site-specific, but they don't really need it, since they are logging into the site through an SSO provider; i.e. Twitter, Facebook, Google LinkedIn, etc.

## Prerequisites (Basic WP Settings)

Before you start, there are two things that must be configured properly in your WP core configuration. Please review these now and get your site prepared for SSO integration; i.e. before continuing into the next sections of this article.

- In order for SSO to work (i.e. for SSO links to appear in your comment/login forms); your [WP Discussion Settings](http://codex.wordpress.org/Settings_Discussion_Screen) should "require users to be logged-in" before posting a comment. Otherwise, there is no reason to log in to begin with, as you don't require user registration at all. If that's the case, we suggest NOT integrating SSO w/ Comment Mail™. It would not serve any useful purpose in such a scenario.

[![2014-11-23_22-55-57](https://cloud.githubusercontent.com/assets/1563559/5161990/eca883de-7363-11e4-894d-632258f89979.png)](https://cloud.githubusercontent.com/assets/1563559/5161990/eca883de-7363-11e4-894d-632258f89979.png)

- You must also "allow users to register" in your [WP General Settings](http://codex.wordpress.org/Settings_General_Screen). Screenshot below. _Note: WP Multisite Network installs can enable user registration from their Network Settings area._

[![2014-11-23_22-54-34](https://cloud.githubusercontent.com/assets/1563559/5161981/c04cad9c-7363-11e4-914e-6584285b0755.png)](https://cloud.githubusercontent.com/assets/1563559/5161981/c04cad9c-7363-11e4-914e-6584285b0755.png)

---

<a id="-services"></a>
## SSO Services (oAuth App Keys/Secrets)

This can be the most time-consuming portion of the integration. Please be patient. Plan to spend at least 30 minutes (perhaps even a couple hours) setting all of these up and tuning things in.

In this article I will cover:

- [Twitter](#-twitter)
- [Facebook](#-facebook)
- [Google](#-google)
- [LinkedIn](#-linkedin)

### First, A Quick Overview...

All of these major services provide an oAuth API which is a common thread that Comment Mail™ works with. However, while each of the services is very much the same, they also differ from each other in subtle ways. For this reason, we suggest that you approach your integration one SSO service at a time. The next sections of this article will approach things in the same way.

Let's get started by integrating with Twitter!

---

<a id="-twitter"></a>
## Twitter SSO Integration

### Step 1. Visit the Twitter Application Center

See: <https://apps.twitter.com/>; sign-in or create a new account.

### Step 2. Create Twitter Web App

[Click here to create a new Web App](https://apps.twitter.com/app/new)

You can put whatever you like for each field, but when it asks for your Callback URL, please use the URL provided by Comment Mail™ in your Dashboard. Comment Mail™ also defines this automatically at runtime, but it's good to configure it properly on the Twitter side too.

Here are a couple of screenshots to show you an example Twitter App.

[![2014-11-23_23-10-44](https://cloud.githubusercontent.com/assets/1563559/5162082/02307278-7366-11e4-8b1f-f45c374f27e4.png)](https://cloud.githubusercontent.com/assets/1563559/5162082/02307278-7366-11e4-8b1f-f45c374f27e4.png)

[![2014-11-23_23-12-49](https://cloud.githubusercontent.com/assets/1563559/5162096/49c3c2b6-7366-11e4-99b9-2fe6e9412c6d.png)](https://cloud.githubusercontent.com/assets/1563559/5162096/49c3c2b6-7366-11e4-99b9-2fe6e9412c6d.png)

### Step 3. Configure App Settings

Once the App has been created, find the "Settings" tab for your new Twitter App, and pull up the current list of details that you just entered. Here you will find an additional config. option that was not available during initial App creation. This box MUST be checked to allow SSO to work w/ Twitter.

[![2014-11-23_23-16-01](https://cloud.githubusercontent.com/assets/1563559/5162109/c080680a-7366-11e4-9e95-7d6f26460dcd.png)](https://cloud.githubusercontent.com/assets/1563559/5162109/c080680a-7366-11e4-9e95-7d6f26460dcd.png)

### Step 4. Obtain oAuth Key/Secret

The last step is to obtain your oAuth Key/Secret for the Twitter App, and give those details to your installation of Comment Mail™. Here are a couple of screenshots to help you with this part.

[![2014-11-23_23-20-03](https://cloud.githubusercontent.com/assets/1563559/5162159/5232795a-7367-11e4-81b9-ffc892645c52.png)](https://cloud.githubusercontent.com/assets/1563559/5162159/5232795a-7367-11e4-81b9-ffc892645c52.png)

[![2014-11-23_23-21-46](https://cloud.githubusercontent.com/assets/1563559/5162166/8ba10698-7367-11e4-8758-a337184e5696.png)](https://cloud.githubusercontent.com/assets/1563559/5162166/8ba10698-7367-11e4-8758-a337184e5696.png)

_[\[back to services list\]](#-services)_

---

<a id="-facebook"></a>
## Facebook SSO Integration

### Step 1. Visit the Facebook Developer Center

See: <https://developers.facebook.com/>; sign-in or create a new account.

### Step 2. Create a New Web App

[Click here to create a new Web App](https://developers.facebook.com/quickstarts/?platform=web)

Facebook simply asks for some basics initially, you can put whatever you like. Once your new Facebook App has been created, fill in your website URL, and mobile URL. Normally the same thing. Then click "Next".

[![2014-11-23_23-35-51](https://cloud.githubusercontent.com/assets/1563559/5162304/1b1cc7e2-736a-11e4-86a8-c917c99ae2b0.png)](https://cloud.githubusercontent.com/assets/1563559/5162304/1b1cc7e2-736a-11e4-86a8-c917c99ae2b0.png)

### Step 3. Move Ahead to Configure Web App

It is tempting to click the "Login" option here, but please skip straight to the Developer Dashboard instead, as the integration between Comment Mail™ and Facebook has already been done by us. All we need is just to edit the App a bit, and obtain the Key/Secret for Comment Mail™ to use.

[![2014-11-23_23-36-47](https://cloud.githubusercontent.com/assets/1563559/5162328/7b67f2a2-736a-11e4-8093-95e2a4f98e1e.png)](https://cloud.githubusercontent.com/assets/1563559/5162328/7b67f2a2-736a-11e4-8093-95e2a4f98e1e.png)

### Step 4. Add List of Approved Domains

Here you should add the domain of the WordPress installation where Comment Mail™ is running; i.e. the domain name for your site.

[![2014-11-23_23-37-42](https://cloud.githubusercontent.com/assets/1563559/5162353/bae0cfa8-736a-11e4-9f69-e2d5312a7e89.png)](https://cloud.githubusercontent.com/assets/1563559/5162353/bae0cfa8-736a-11e4-9f69-e2d5312a7e89.png)

### Step 5. Obtain oAuth Key/Secret

The last step is to obtain your oAuth Key/Secret for the Facebook App, and give those details to your installation of Comment Mail™. Here are a couple of screenshots to help you with this part.

[![2014-11-23_23-38-20](https://cloud.githubusercontent.com/assets/1563559/5162366/ddd74104-736a-11e4-9183-379aa6a1512e.png)](https://cloud.githubusercontent.com/assets/1563559/5162366/ddd74104-736a-11e4-9183-379aa6a1512e.png)

[![2014-11-23_23-47-39](https://cloud.githubusercontent.com/assets/1563559/5162384/2779e802-736b-11e4-9cc1-930c7f28d62d.png)](https://cloud.githubusercontent.com/assets/1563559/5162384/2779e802-736b-11e4-9cc1-930c7f28d62d.png)

_[\[back to services list\]](#-services)_

---

<a id="-google"></a>
## Google SSO Integration

### Step 1. Visit the Google Developer Console

See <https://console.developers.google.com>; sign-in or create a new account.

### Step 2. Create a New Project

Once you're logged-in, click the "Create Project" button.

[![2014-11-23_23-52-22](https://cloud.githubusercontent.com/assets/1563559/5162455/ce96ebc6-736b-11e4-9e3c-8651308fd45a.png)](https://cloud.githubusercontent.com/assets/1563559/5162455/ce96ebc6-736b-11e4-9e3c-8651308fd45a.png)

Google just asks for some basics. You can enter whatever you like. When you're done, click the "Create" button and wait for your new Web App to show up in the list on this page, or for the Project Dashboard page to open automatically.

[![2014-11-23_23-53-51](https://cloud.githubusercontent.com/assets/1563559/5162471/00a1f322-736c-11e4-8ab2-e03c96fde73f.png)](https://cloud.githubusercontent.com/assets/1563559/5162471/00a1f322-736c-11e4-8ab2-e03c96fde73f.png)

### Step 3. Configure the App (i.e., Project)

Once the App (Project) has been created, find the "APIs & Auth" section in the Project Dashboard. Click to edit your "Consent Screen". This is what people will see when your site requests access to their account for the purpose of signing them in automatically. You can tune this in however you like. For now, just enter some of the basics to get a Consent Screen created, so that you can move on to the next step.

[![2014-11-23_23-57-00](https://cloud.githubusercontent.com/assets/1563559/5162501/77ac6bdc-736c-11e4-9103-973582a070bf.png)](https://cloud.githubusercontent.com/assets/1563559/5162501/77ac6bdc-736c-11e4-9103-973582a070bf.png)

### Step 4. Create Client ID for Authentication

Now we need to create a new Client ID. Find the "APIs & Auth" section in the Project Dashboard. Click to edit "Credentials", and then choose "Create Client ID". You will be asked for a Callback URL, which you can obtain from your Comment Mail™ installation via the WP Dashboard. I'm attaching some screenshots to help you with this part.

[![2014-11-24_00-00-15](https://cloud.githubusercontent.com/assets/1563559/5162532/e64bc380-736c-11e4-8775-e195371eb160.png)](https://cloud.githubusercontent.com/assets/1563559/5162532/e64bc380-736c-11e4-8775-e195371eb160.png)

[![2014-11-24_00-03-21](https://cloud.githubusercontent.com/assets/1563559/5162585/98923dda-736d-11e4-8c2d-a7820c73b040.png)](https://cloud.githubusercontent.com/assets/1563559/5162585/98923dda-736d-11e4-8c2d-a7820c73b040.png)

[![2014-11-24_00-04-04](https://cloud.githubusercontent.com/assets/1563559/5162574/6ec1ea96-736d-11e4-99b4-c4aa5e3106d5.png)](https://cloud.githubusercontent.com/assets/1563559/5162574/6ec1ea96-736d-11e4-99b4-c4aa5e3106d5.png)

### Step 5. Obtain oAuth Key/Secret

The last step is to obtain your oAuth Key/Secret for the Google App (Project), and give those details to your installation of Comment Mail™. Here are a couple of screenshots to help you with this part.

[![2014-11-24_00-06-33](https://cloud.githubusercontent.com/assets/1563559/5162614/fa6cff4a-736d-11e4-811a-86540d65cc7e.png)](https://cloud.githubusercontent.com/assets/1563559/5162614/fa6cff4a-736d-11e4-811a-86540d65cc7e.png)

[![2014-11-24_00-07-51](https://cloud.githubusercontent.com/assets/1563559/5162615/fa917384-736d-11e4-9eda-5cbc0eff6467.png)](https://cloud.githubusercontent.com/assets/1563559/5162615/fa917384-736d-11e4-9eda-5cbc0eff6467.png)

_[\[back to services list\]](#-services)_

---

<a id="-linkedin"></a>
## LinkedIn SSO Integration

### Step 1. Visit the LinkedIn Developer Network

See: <https://developer.linkedin.com/>; sign-in or create a new account.

### Step 2. Create New Application

Once you're logged-in, click the "Add New Application" link from [this page](https://www.linkedin.com/secure/developer).

[![2014-11-24_00-21-43](https://cloud.githubusercontent.com/assets/1563559/5162772/e840410e-736f-11e4-9844-eafdb0309442.png)](https://cloud.githubusercontent.com/assets/1563559/5162772/e840410e-736f-11e4-9844-eafdb0309442.png)

LinkedIn asks for a whole bunch of information when you create a new App. Not all of these fields are required; and in fact, many of them are unnecessary for what we want to do with LinkedIn here.

LinkedIn will ask for your oAuth 2.0 Callback URL, so it's a good idea to get this ready. You can find this in your Comment Mail™ options from the WP Dashboard. Here is a screenshot to help you out.

[![2014-11-24_00-31-33](https://cloud.githubusercontent.com/assets/1563559/5162882/7eee10ee-7371-11e4-86d6-79e446f69674.png)](https://cloud.githubusercontent.com/assets/1563559/5162882/7eee10ee-7371-11e4-86d6-79e446f69674.png)

Here is a screenshot of the New App form that has been filled-in already. This should give you some idea of what is necessary and what is not. It's important to check the `r_basicprofile` and `r_emailaddress` boxes. These are the permissions that Comment Mail™ needs to log a user in automatically.

[![2014-11-24_00-32-04](https://cloud.githubusercontent.com/assets/1563559/5162883/7f1e27b6-7371-11e4-87d7-9d325140606c.png)](https://cloud.githubusercontent.com/assets/1563559/5162883/7f1e27b6-7371-11e4-87d7-9d325140606c.png)

### Step 3. Obtain oAuth Key/Secret

Once the App has been created, you will be presented with the following screen. The last step is to take your oAuth Key/Secret for the LinkedIn App you just created, and give those details to your installation of Comment Mail™. Here are a couple of screenshots to help you with this part.

_Note: You may find it tempting to copy/paste the wrong Token/Secret from this page. Please be careful about which set of credentials you use. LinkedIn provides both oAuth 1.0a and 2.0 credentials. The set on the bottom is for oAuth version 1.0a. What you need are the v2.0 credentials on top._

[![2014-11-24_00-35-18](https://cloud.githubusercontent.com/assets/1563559/5163088/8e7eac88-7373-11e4-83ab-c34a65312d61.png)](https://cloud.githubusercontent.com/assets/1563559/5163088/8e7eac88-7373-11e4-83ab-c34a65312d61.png)

[![2014-11-24_00-46-00](https://cloud.githubusercontent.com/assets/1563559/5163056/4e3ebcda-7373-11e4-8b95-537d09b13725.png)](https://cloud.githubusercontent.com/assets/1563559/5163056/4e3ebcda-7373-11e4-8b95-537d09b13725.png)

_[\[back to services list\]](#-services)_
