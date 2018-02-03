---
author: h0lyalg0rithm
comments: true
date: 2015-01-03 06:07:02+00:00
layout: post
link: http://surajms.com/2015/01/setting-amazon-s3-permissions/
slug: setting-amazon-s3-permissions
title: Setting up Amazon S3 permissions
wordpress_id: 225
categories:
- DevOps
---

Amazon S3 is a really powerful data store.S3 works by grouping content in buckets. If you have a lot of buckets on amazon it is not feasible or secure to use your own security access key with the buckets(Especially if you have to handover the project).
Moreover there is no official way to transfer s3 buckets from one aws account to another.The best way is to create a bucket on the clients account and only provide the appropriate permission on the bucket.
Amazon lets you define permission through their iam policy.IAM policy has 3 keys which define your permission.
These where take right from the amazon docs.

**Actions**: what actions you will allow. Each AWS service has its own set of actions. For example, you might allow a user to use the Amazon S3 ListBucket action, which returns information about the items in a bucket. Any actions that you don't explicitly allow are denied.

**Resources**: which resources you allow the action on. For example, what specific Amazon S3 buckets will you allow the user to perform the ListBucket action on? Users cannot access any resources that you have not explicitly granted permissions to.

**Effect**: what the effect will be when the user requests access—either allow or deny. Because the default is that resources are denied to users, you typically specify that you will allow users access to resource.

Here is the IAM Policy that  I use to restrict a user to a particular bucket.It gives user all the permission over the bucket ie to Add,Delete,List...

    
    {
      "Version": "2014-10-17",
      "Statement": [
        {
          "Effect": "Allow",
          "Action": "s3:*",
          "Resource": [
           "arn:aws:s3:::<bucket-name>",
           "arn:aws:s3:::<bucket-name>/*"
          ]
        }
      ]
    }
    Just replace <bucket-name> with your s3 bucket name.



