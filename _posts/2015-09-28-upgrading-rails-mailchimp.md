---
layout: post
title: Mailchimp + Gibbon + Seed: A Match Made in Heaven
---

Why we need this
-------------------------
Mailing lists enable start ups to reach their audience and help users find out about useful products. This article will help you build the first piece of your marketing machine with lightning speed.

Getting Started
-------------------------

Gibbon & Mailchimp provide you with list managment tools and a simple CMS for crafting your message. While Happy Seed provided the tools to spin it up on a live server.

If you are new to Mailchimp/Gibbon/Rails, check out <a href="http://cheshireoctopus.github.io/blog/2014/01/23/mailchimp-plus-gibbon-plus-rails-create-a-basic-sign-up-form/" target="_blank">this article</a> for an overview.

Learn more about Seed <a href="http://seed.happyfuncorp.com/" target="_blank">here.</a>

![mt path](http://earlyblogger.com/wp-content/uploads/2015/03/mailchimp.jpg)

Mailchimp Setup
-------------------------
The steps for setting up Mailchimp will remain unchanged. You'll need a Mailchhimp API key, an email list, and the corresponding list id. See <a href="http://cheshireoctopus.github.io/blog/2014/01/23/mailchimp-plus-gibbon-plus-rails-create-a-basic-sign-up-form/" target="_blank"> Part One</a> for reference.

Planting Seeds
-------------------------
Seed is intuitive an powerful. To create a new app:
```
happy_seed rails APP-NAME
```

The application will run bundle automatically as prompt you to install a handful of generators. 'Splash' is necessary.

Happy Seed uses <a href "https://github.com/bkeepers/dotenv" target="_blank">dotenv</a> to mangage environment variables by default. Once your app is generated, add you MAILCHIMP_API_KEY and and MAILCHIMP_SPLASH_LIST_ID to the .env file.

''' yaml
AWS_ACCESS_KEY_ID=
AWS_SECRET_ACCESS_KEY=
S3_BUCKET_NAME=
HTTP_AUTH_USERNAME=
HTTP_AUTH_PASSWORD=
GOOGLE_ANALYTICS_SITE_ID=
MAILCHIMP_API_KEY=481241:7:8bf5441754d39b65g3:1232.vt22
MAILCHIMP_SPLASH_SIGNUP_LIST_ID=07c087a8ab
```

Restart the server and you can confirm your environment variables are present using the console.

Seed for Mailchimp API 3.0 and Gibbon 2.0
-------------------------

Mailchimp and Gibbon were recently updated and you'll need to make a few change to your controller before going live with your new mailing list.

In app/controllers/splash_controller.rb replace:

```
gb = Gibbon::API.new

gb.lists.subscribe({
	:id => ENV['MAILCHIMP_SPLASH_SIGNUP_LIST_ID'],
	:email => {:email => params[:signup_email]},
	:double_optin => true
})
```
with:

```
gb = Gibbon::Request.new(api_key: ENV['MAILCHIMP_API_KEY'])

gb.lists(ENV['MAILCHIMP_SPLASH_SIGNUP_LIST_ID']).members.create(
	body: {
		email_address: params[:signup_email], 
		status: "pending"
	}
)
```

We no longer submit :double_optin => true. Instead, the status: "pending" indicate that a user must respond to a confirmation their subscribtion to you email list.

While the gibbon gem documentation used status: "subscribed", this will automatically sign users up. Which option you choose will depend on your use cases.

This is intended as a basic introduction to what you can do with <a href="http://kb.mailchimp.com/api">Mailchimp</a>+ <a href="https://github.com/amro/gibbon">Gibbon</a> + <a href="seed.happyfuncorp.com">Seed</a>. Check out the linked documentation to explore the full functionality of these technologies.




