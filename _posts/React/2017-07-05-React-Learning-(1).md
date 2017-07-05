---
layout: post
category : ReactJS
tagline: "Supporting tagline"
tags : [ReactJS,Frontend]
---
{% include JB/setup %}

### Installation

Using CDN.

~~~
<script src="https://unpkg.com/react@15/dist/react.js"></script>
<script src="https://unpkg.com/react-dom@15/dist/react-dom.js"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/babel-core/5.8.24/browser.js"></script>
~~~

First two is react lib, and the third one is allowing you to write html in `<script></script>`.


### HelloWorld!

The main idea is first create a class, then render it in HTML.

Let's first add a div in HTML.

~~~
    <div id="example"></div>
~~~

Then create a class in `<script></script>`

~~~
    <script type="text/babel">

        class HelloWorld extends React.Component {
            render(){
                return(
                    <h1>Hello World!</h1>
                );
            }
        }

        ReactDOM.render(< HelloWorld />, document.getElementById('example'));
        
    </script>
~~~

As we can see, the class is called HelloWorld, and it extends from `React.Component`, you could add any HTML inside of this component. `ReactDOM.render()` will render `HelloWorld` class back to `<div id="example"></div>`.

Results:

<img src="/assets/photos/ReactLearn-1.png" alt="1" style="width: 630px; margin: 0 auto; display:block;"/>

### Props

The previous React class is static, the content cannot be changed. But what if we want it could be changed? By passing a parameter?

Use `Props`!

~~~
ReactDOM.render(< HelloWorld name="Charles"/>, document.getElementById('example')); 
~~~

Simply add a name property, and modify our `HelloWorld` class.


~~~
        class HelloWorld extends React.Component {
            render(){
                return(
                    <div>
                        <h1>Hello World!</h1>
                        <h2>{this.props.name}</h2>
                    </div>
                );
            }
        }
~~~

Attention:    
* Inside of `return()` method, there could be only one tag. so put a `<div>` tag to cover all other two tags.
* Writing javaScript inside of HTML tag is simple, use `{}` and put javaScript inside.

<img src="/assets/photos/ReactLearn-2.png" alt="2" style="width: 630px; margin: 0 auto; display:block;"/>

