---
layout: post
category : AWS
tagline: "Supporting tagline"
tags : [SSH,AWS]
---
{% include JB/setup %}

### Getting Started

AWS Lightsail allows users to deploy an application on a cloud server without any of the additional services normally included in AWS.

### Create an instance

Login to AWS Lightsail, Create an instance.

<img src="/assets/photos/Lightsail-1.png" alt="lightsail-1" style="width: 630px; margin: 0 auto; display:block;"/>

### Download your default key.

AWS will create a default SSH key pairs for you to use to connect.

Go to `Account` page and `SSH keys`. Download the `.pem` file to your computer.

<img src="/assets/photos/Lightsail-2.png" alt="lightsail-2" style="width: 630px; margin: 0 auto; display:block;"/>

Copy your SSH key pairs to `~/.ssh/`.

### Connect by terminal

use `ssh -i ~/.ssh/myKey.pem user@xx.xx.xx.xx` you will be connected with your cloud server!

<img src="/assets/photos/Lightsail-3.png" alt="lightsail-3" style="width: 630px; margin: 0 auto; display:block;"/>



