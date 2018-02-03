---
author: h0lyalg0rithm
comments: true
date: 2016-07-22 19:35:48+00:00
layout: post
link: http://surajms.com/2016/07/sending-sms-cheap/
slug: sending-sms-cheap
title: Sending SMS for cheap
wordpress_id: 4741
categories:
- Ruby
- Yapp
---

Whenever we think about integrating sms in our application, the only company that comes to comes to is twilio. Twilio is a really good service however they are relatively expensive to their competitors especially if you know where your target audience is from.

In my case I was working for startup in Spain which operated in the Spain/Portugal region.For a while we were using twilio, but soon the number of sms we were sending grow to huge amount and we were spending a significant amount of money on it.

We came across another provider smsgateway.to .Compared to Twilio it wasnt a very popular provider but its pricing was much better.We gave this a provider a try and tested sending SMS through them.Their delivery rate was pretty high and we decided to switch to them.We came across another issue, they didnt have a ruby client so I wrote a quick one and was ready to use it production.

We are now using the service in production for 2 months and we have had no issue so far.More over we reduced the cost of our sms by more than 3 times.

The library is available at [https://github.com/h0lyalg0rithm/sms_gateway_to](https://github.com/h0lyalg0rithm/sms_gateway_to)
