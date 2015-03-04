---
layout:    post
title:     "Adding a Custom Domain Name to Your Amazon S3 Website"
date:      2015-03-04 22:05:37
published: true
---
The Domain Name System (DNS) is something that nearly everyone relies on every single day. It underpins the Internet, going about its business largely unnoticed, transforming human readable names into numerical IP addresses. 

Why should you care about DNS? [Your Amazon S3 website][static-website] is fanastic, the content is sublime, it's brilliantly designed, and would be the darling of the Internet if only people could remember the URL. Unfortunately something like [http://cookery.today.s3-website-eu-west-1.amazonaws.com][cookery-today-s3] doesn't trip off the tongue. Let's fix that.

## Before Taking the Plunge

What follows assumes that you've just purchased a brand new shiny domain name and don't have any existing configuration. Proceed with caution if you're hosting an existing website, and **especially** if you use your domain for email.

## Taking the Registrar

You purchased your domain name through a Registrar. Names like Hover, Network Solutions, and 123Reg might be familiar. Your registrar will have a Web interface which will allow you to alter the Name Servers for your domain. 

![Name Servers]({{ site.url }}/assets/custom-domain/nameservers.png)

In the screenshot above, the name servers for cookery.today are ns1.hover.com and ns2.hover.com. These are computers on the Internet which hold the authoritative information for your domain. Things like which computer your website is running on and where to send your email. 

I'm going to change these to give Amazon's Route 53 service control.

[static-website]: /2015/02/28/hosting-a-website-on-amazon-s3.html
[cookery-today-s3]: http://cookery.today.s3-website-eu-west-1.amazonaws.com