---
layout: post
category : ASP.NET
tagline: "Supporting tagline"
tags : [ASP.NET,Razor,Javascript]
---
{% include JB/setup %}

It is really easy, but it is important, so I want to write it down here.

In Javascript block
~~~
<Script>
    Javascript here
    @{
        Razor here just like outside.
        <text>
            javascript here.
        </text>
    }
</Script>
~~~

As we can see, with a `@{...}`, you could use values in Model or Viewdata[] just like the same in View.

### One Thing need to be notice while passing value from Model to Javascript var!

In Javascript block, suppose `var s` is a string, you cannot do `var stringInScript = @s`, the right way to do it is by `var stringInScript = "@s"`, add `" "` between the string value. Then you'll get what you want!