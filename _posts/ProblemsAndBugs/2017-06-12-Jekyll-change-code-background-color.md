---
layout: post
category : problems and bugs
tagline: "Supporting tagline"
tags : [jekyll,css,github]
---
{% include JB/setup %}

##Change Jekyll theme code background color

Locate to `./assets/themes/themeName/css/style.css`    
change `background-color` in following codes 
~~~~~~~
.unit-article li code {
  padding: 2px 5px;
  white-space: nowrap;
  background-color: #e6e6e6;
}
~~~~~~~

Done!!