---
layout: post
category : problems and bugs
tagline: "Supporting tagline"
tags : [Javascript]
---
The method `.new Date()` in Javascript, will use the server time zone. It will cause issue when this time need to be passed and communicated with client time.

The way to fix this is by `getTimezoneOffset()` method, this method will return the difference between local time and UTC time, return value is in minutes. This `value*60*1000` will transfer minutes to millisecond, which is used for Javascripte time variable.

By doint following, this bug can be fixed.

~~~
eDate.setTime(eDate.getTime() + eDate.getTimezoneOffset()*60*1000);
~~~