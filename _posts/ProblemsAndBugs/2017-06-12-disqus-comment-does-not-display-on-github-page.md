---
layout: post
category : Problems and bugs
tagline: "Supporting tagline"
tags : [jekyll,disqus,github]
---
{% include JB/setup %}

## Problem discription
Having a problem that while using disqus commenting, runs perfectly on local, but does not display on github page.

## Reason
Github is using HTTPS and Disqus was being served over HTTP.

## Solution
Edit Disqus comment provider `_includes/JB/comments-providers/disqus`, change the URL to `HTTPS://`.
`dsq.src = 'https://' + disqus_shortname + '.disqus.com/embed.js';`.

The problem would be solved! 