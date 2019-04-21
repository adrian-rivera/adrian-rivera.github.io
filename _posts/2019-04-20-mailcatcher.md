---
title: Setting up an email service for your development environment
---
I'm almost certain that most applications will come to a point where they are required to communicate with an individual, and most of the time this communication is done using an email, but in this post I'm not talking about how to make this integration with your app, there are many resources for that, here we are going to talk about how to run an small email service for you local environment using [MailCatcher](https://mailcatcher.me).

Ok, why on earth would you want to do that? You could simply put your STMP personal credentials on your configuration, or integrate with an extra service just for your developer needs, sure you could do that, but now think on the other problems that you will face:

* **Latency**: It will take a few seconds while your app prepares your email, then
  send it over the internet, and then your email server needs to receive the
  call process the whole thing and store it, by this moment you have hit the
  refresh button at least 6 times, because, as usual, you are in a rush.

* **Need for Internet**: If you want to test your app, you'd need to have an stable
  internet connection, which can be faulty if your are in your favorite coffee
  place, or sometimes even at work, and you don't want to go through the hassle
  of sharing your mobile data with your laptop just to send emails that you may
  or not need.

* **A real email**: You would need a real email address on a functional site to
  test every single email that you want to send.

* **Your very long email address**: This is a problem because in the case you are
  working in a *sign-up* page you may not allow different users to have the same
  email, therefore your first user's email is:
  `first_name_last_name@my_company.com`
  great!, now your second user's email is:
  `first_name_last_name+my_test@my_company.com`
  great!, now your third user's email is:
  `first_name_last_name+another_test@my_company.com`
  and now you see my point, your are going to end up with tons of unnecessary
  emails on your inbox for no good reason. 

* **Security**: You are a developer, you are developing stuff, and with that you
  are eligible to create bugs, bugs which can have big consequences if by any
  chance you add extra data to an email body, and send it to your list of emails
  in your local db which they should not be real, but they kind-of-actually
  are because you needed to test your email feature.

Because of all these issues, and maybe more that I haven't thought, you need some
tool that let's you work offline, isolated from the internet, with no need for
a real email address, and this is a perfect use case for a tool like
MailCatcher, this app creates a simple SMTP server that runs locally, all the
emails send through that server are going to be available in your browser.

## Install & Configure

MailCatcher uses [Ruby](https://www.ruby-lang.org/en/) to run, this doesn't mean that your app needs to be on
Ruby, only MailCatcher will require this.

### Prerequisites
* Ruby >= 2.0.0, based on [RubyGems](https://rubygems.org/gems/mailcatcher)



