---
layout: post
title: "Hosting a Website on Amazon S3"
categories: amazon-s3
---
This is a basic guide covering how to host a static website using Amazon's S3 service. Subsequent guides will delve into Jekyll (a static site generator), configuring a custom domain name for your site, and speeding up access to your site by adding support for the Amazon CloudFront content delivery network.

## Getting Started

First, you’ll need an Amazon Web Services Account to begin, pop along to the [AWS site][aws] and sign up there. You’ll need to enter a credit card number and go through Amazon’s telephone verification process. Although Amazon offer a very generous free tier for a year, there are limits in place which are chargeable should they be exceeded. Fortunately, Amazon is makes their [pricing available][s3-pricing]. 

## OK, I’ve Signed Up

Excellent, then log in to the [AWS Management Console][management-console] and browse to ‘Services’ then ’S3’. Amazon S3 stores files in containers called ‘Buckets’. Buckets need to have a globally unique name that conforms to a number of [restrictions][bucket-restrictions]. Basically, name the buckets after your web site (if the name is available) as follows, and all should be fine.

You’ll need two buckets to host your website. I’m going to set up a new site called cookery.today and will create the following buckets.

* __logs.cookery.today__
* __cookery.today__

The buckets all have different purposes - __cookery.today__ will contain the content and __logs.cookery.today__ will store the website access logs.

Create the ‘logs’ bucket first. You’ll see why in a minute. When asked to choose a region, it’s probably best to select one closest to where the majority of your viewers live. When adding you main website bucket, click ’Set Up Logging’ and choose your [logs bucket][logs-bucket].

## There’s a Hole in My Bucket

Now you have created the buckets, it’s time to upload some content and enable web access.

Copy the following text, and create two new files on your computer called ‘index.html’ and ‘error.html’.

### index.html

{% highlight html %}
<html>
  <head>
    <title>My Amazon S3 Website</title>
  </head>
  <body>
    <h1>My Amazon S3 Website</h1>
  </body>
</html>
{% endhighlight %}

### error.html

{% highlight html %}
<html>
  <head>
    <title>Error!</title>
  </head>
  <body>
    <h1>Sorry, an error has occurred.</h1>
  </body>
</html>
{% endhighlight %}

Click on your web content bucket (**cookery.today** in my case), and then click ‘Upload’. Choose your index.html and error.html files and then click ’Start Upload’.

[aws]: https://aws.amazon.com
[s3-pricing]: https://aws.amazon.com/s3/pricing/ 
[management-console]: http://console.aws.amazon.com
[bucket-restrictions]: http://docs.aws.amazon.com/AmazonS3/latest/dev/BucketRestrictions.html
[logs-bucket]: {{ site.url }}/assets/s3-website/enable-logging.png
