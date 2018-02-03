---
author: h0lyalg0rithm
comments: true
date: 2015-04-02 17:22:12+00:00
layout: post
link: http://surajms.com/2015/04/setting-up-different-builds-for-android/
slug: setting-up-different-builds-for-android
title: Setting up different builds for android
wordpress_id: 378
categories:
- Android
- Java
---

A year ago google released android studio.An IDE based on intellij.They also introduced a task runner to build your applications, run test and manage dependencies.

Gradle is the task runner and it supports a Java,Android and C/C++ projects.That what they claim on their website.But for this post I will be dealing with android.

The android gradle project has buildTypes which are equivalent to environments in the backend development world.Android has 2 by default one is debug the other is release.You can specify more buildtypes based on your application.

You can easily create another buildtype

    
    signingConfigs {
            prerelease {
                storeFile file("prerelease.keystore")
                storePassword "<your password>"
                keyAlias "<key.alias>"
                keyPassword "<your password>"
            }
        } 
    buildTypes {
            prerelease {
                minifyEnabled false
                proguardFiles getDefaultProguardFile('proguard-android.txt'), 'proguard-rules.pro'
                signingConfig signingConfigs.prerelease
            }
        }


You need to add the signingConfig this way it will build and sign the keys before installing.

By default the Install<Buildtype> doesn't show and the only way to show it is to have signingConfig specified in the buildtype.

Here are the other options available to each buildtype

If a property is not set through the DSL, some default value will be used. Here’s a table of how this is processed.


<table cellspacing="0" border="1" >
<tbody >
<tr >

<td > Property Name
</td>

<td > Default value in DSL object
</td>

<td > Default value
</td>
</tr>
<tr >

<td > **versionCode**
</td>

<td > -1
</td>

<td > value from manifest if present
</td>
</tr>
<tr >

<td > **versionName**
</td>

<td > null
</td>

<td > value from manifest if present
</td>
</tr>
<tr >

<td > **minSdkVersion**
</td>

<td > -1
</td>

<td > value from manifest if present
</td>
</tr>
<tr >

<td > **targetSdkVersion**
</td>

<td > -1
</td>

<td > value from manifest if present
</td>
</tr>
<tr >

<td > **applicationId**
</td>

<td > null
</td>

<td > value from manifest if present
</td>
</tr>
<tr >

<td > **testApplicationId**
</td>

<td > null
</td>

<td > applicationId + “.test”
</td>
</tr>
<tr >

<td > **testInstrumentationRunner**
</td>

<td > null
</td>

<td > android.test.InstrumentationTestRunner
</td>
</tr>
<tr >

<td > **signingConfig**
</td>

<td > null
</td>

<td > null
</td>
</tr>
<tr >

<td > **proguardFile**
</td>

<td > N/A (set only)
</td>

<td > N/A (set only)
</td>
</tr>
<tr >

<td > **proguardFiles**
</td>

<td > N/A (set only)
</td>

<td > N/A (set only)
</td>
</tr>
</tbody>
</table>
Source: [Google](http://tools.android.com/tech-docs/new-build-system/user-guide)

By default gradle looks for the keystore file in the **app/** directory.

You can also run multiple gradle jobs in parallel, by setting the following in the gradle.properties file.

    
    org.gradle.parallel=true


Using buildtype can improve overall code quality especially if you have multiple config data like server urls.

To override a particular file for a particular build all you have to is create a folder in the **src/** directory.

[![tree](http://surajms.azurewebsites.net/wp-content/uploads/2015/04/tree.png)](http://surajms.azurewebsites.net/wp-content/uploads/2015/04/tree.png)
