---
title: Setting up an email service for your development environment
tags: [dev, ruby]
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

### Installation

The installation is really simple you just need to run
```shell
gem install mailcatcher
```
And that is it, the gem command will install all the internal dependencies for
MailCatcher.

### Run
The simplest way to make it run is just to invoke the command
```shell
mailcatcher
```
After running this you'll see a small prompt with the default for this execution
```shell
Starting MailCatcher
==> smtp://127.0.0.1:1025
==> http://127.0.0.1:1080/
*** MailCatcher runs as a daemon by default. Go to the web interface to quit.
```
By default MailCatcher SMTP port is `1025` and the browser port is `1080`, if we
access `http://127.0.0.1:1080` you'll be able to see MailCatcher running.
![MailCatcher ScreenShot](/assets/img/2019_04_20/browser-01.png)

To quit MailCatcher you can kill the process or press the `Quit` button on the
browser.

In case you want to run MailCatcher in a different port, let's say `2050` for
SMTP and `2080` for HTTP then you should execute the command like this:
```shell
mailcatcher --smtp-port 2050 --http-port 2080
```

For more options run:
```shell
mailcatcher -h
```

### Configure your app

This section depends a lot on you application, so I'll just cover how to
configure a simple rails app in here, but don't be afraid for most applications
you'll only need the following data:
* SMTP Address: `127.0.0.1`
* SMTP Port: `1025`
* SMTP User: `ANYTHING_YOU_WANT`
* SMTP Password: `ANYTHING_YOU_WANT`

It is important to say that MailCatcher won't require you to send any kind of
authentication, remember that you should only use this in your dev environment,
therefore you can put anything, or nothing, as `user/password` combo.

For a simple rails application you only need to configure your
`enviroments/development.rb` file with:
```ruby
config.action_mailer.delivery_method = :smtp
config.action_mailer.smtp_settings = { :address => "localhost", :port => 1025 }
```
And that's it, rails will start using MailCatcher.

Here is an example of an email on MailCatcher:
![First Email](/assets/img/2019_04_20/browser-02.png)

## Finally
And this is how I conclude this post, I hope that you can find this helpful and
use it in your current project.

## Links
* [MailCatcher](https://mailcatcher.me)
* [MailCatcher Github's Page](https://github.com/sj26/mailcatcher)

