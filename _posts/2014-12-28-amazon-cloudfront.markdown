---
author: h0lyalg0rithm
comments: true
date: 2014-12-28 18:24:39+00:00
layout: post
link: http://surajms.com/2014/12/amazon-cloudfront/
slug: amazon-cloudfront
title: Amazon cloudfront
wordpress_id: 217
categories:
- DevOps
---

Last month I wrote a post of saving bandwidth costs on Amazon but using nginx as a reverse proxy for Amazon s3.After doing some further research I came across cloudfront.Cloudfront is a CDN offering from the web services giant Amazon.

Cloudfront integrates really well with Amazon S3.Apart from the initial setup which migrated your s3 data to the CDN (Which took about 30mins).The rest of the process was straight forward.The CDN took care of loading data from s3 and the performance benefits where huge.

Previously a 200kb file would take about 8-10 seconds to download directly from s3.
Using cloudfront dropped the time down to 2-3 secs that's close to 4x improvement.

I would highly recommend using cloudfront.To sweeten things up Amazon also provides a nice dashboard showing the different requests,hit rate misses errors.
