---
layout: post
title: "Hosting a Website on Amazon S3"
published: true
---
This is a basic guide covering how to host a static website using Amazon's S3 service. Subsequent guides will delve into Jekyll (a static site generator), configuring a custom domain name for your site, and speeding up access to your site by adding support for the Amazon CloudFront content delivery network.

## Getting Started

First, you’ll need an Amazon Web Services Account to begin. Pop along to the [AWS site][aws] and sign up there. You’ll need to enter a credit card number and go through Amazon’s telephone verification process. Although Amazon offer a very generous free tier for a year, there are limits in place which are chargeable should they be exceeded. Fortunately, Amazon is makes their [pricing available][s3-pricing]. 

## OK, I’ve Signed Up

Excellent, then log in to the [AWS Management Console][management-console] and browse to ‘Services’ then ’S3’. Amazon S3 stores files in containers called ‘Buckets’. Buckets need to have a globally unique name that conforms to a number of [restrictions][bucket-restrictions]. Basically, name the buckets after your web site (if the name is available), and all should be fine.

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

![Select files to upload]({{ site.url }}/assets/s3-website/select-files.png)

After you file have uploaded, click the ‘Properties’ button at the top-right of the screen, find the ’Static Website Hosting’ section, choose the ‘Enable website hosting’ option and enter the filenames for the index and error documents. Take a note of the part marked ‘Endpoint’. This is the URL that your website will be published to.

![Select files to upload]({{ site.url }}/assets/s3-website/static-web-hosting.png)

You’ll receive an error message if you try to access that URL right now. You need to change the bucket permissions to enable viewers to see the content. Find the ‘Permissions’ section (it’s above the ’Static Website Hosting’ bit), then click the ‘Edit bucket policy’ button. Enter the policy below substituting the cookery.today part with the name of your bucket.

### Bucket Policy

{% highlight json %}

{
	"Version": "2012-10-17",
	"Statement": [
		{
			"Sid": "Allow Public Access to All Objects",
			"Effect": "Allow",
			"Principal": "*",
			"Action": "s3:GetObject",
			"Resource": "arn:aws:s3:::cookery.today/*"
		}
	]
}

{% endhighlight %}

Click ‘Save’ and visit your endpoint URL. You should see your index page. 

Although this works, uploading content isn’t ideal and the endpoint URLs really aren’t friendly. I’ll address both issues in later posts.

[aws]: https://aws.amazon.com
[s3-pricing]: https://aws.amazon.com/s3/pricing/ 
[management-console]: http://console.aws.amazon.com
[bucket-restrictions]: http://docs.aws.amazon.com/AmazonS3/latest/dev/BucketRestrictions.html
[logs-bucket]: {{ site.url }}/assets/s3-website/enable-logging.png
