---
layout: post
title: "Use Mailcatcher During Development!"
date: 2015-04-29 11:35
tags: development mail mailcatcher
comments: true
---
Oddly enough, I just started using [Mailcatcher][0] during my daily
development work. I say *oddly enough* because I spent most of my time at my
previous job working with email services and sending massive amounts of email.
I actually used [smtp4dev][1] back then, but I'm no longer on Windows and never
sought out an alternative. 

What Mailcatcher does is intercept **all** emails sent from your application
and allow you to inspect them in a nice web interface without ever having
actually sent anything to an external mail server. It's pure genius and if your
application is sending emails you *should* be using it!

##Benefits:

- No more flooding your personal/work inbox with emails.
- Never accidentally send an email to someone you wished you hadn't from your
development environment(*this happens far more often than I'd like to admit*).
- Dead simple setup(especially for Rails).
- No setup of an external mail server or email provider for development and
local testing.

If you're curious on how to get started with Mailcatcher, the project [website]
[1] provides dead simple steps to get going(blatantly copied below!).

1. `gem install mailcatcher`
1. `mailcatcher`
1. Go to http://localhost:1080/
1. Send mail through smtp://localhost:1025

If your using Rails add this to your environments/development.rb
{% highlight ruby %}
config.action_mailer.delivery_method = :smtp
config.action_mailer.smtp_settings = { :address => "localhost", :port => 1025 }
{% endhighlight %}

[0]: http://mailcatcher.me/ "Mailcatcher"
[1]: http://smtp4dev.codeplex.com/ "smtp4dev"
[2]: {{ site.url }}/assets/mailcatcher.png "Mailcatcher UI"
