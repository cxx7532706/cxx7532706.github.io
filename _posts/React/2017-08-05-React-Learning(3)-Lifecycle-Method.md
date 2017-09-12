---
layout: post
category : ReactJS
tagline: "Supporting tagline"
tags : [ReactJS,Frontend]
---
{% include JB/setup %}

## Two Lifecycle Methods to a Class

Lifecycle Methods are used for components that need to be freed up resources when destroyed.

To help understand those methods, here I take an example of a lifecycle timer that runs all the time while component exsits.

### 1. componentDidMount()

This method will be called when react finish rendered a component, which is good to use for initialization.

First add display dateTime HTML in component render().

~~~
render(){
    const styleObj = {
        backgroundColor: this.state.color
    };

    return(
        <div style={styleObj} >
            <h1>Hello World!</h1>
            <h2>{this.props.name}</h2>
            <h2>It is {this.state.date.toLocaleTimeString()}. </h2>
            <button onClick={this.toogleColor}>ToggleColor</button>
        </div>
    );
}
~~~

Then add timer in componentDidMount().

~~~
componentDidMount(){
    this.timerID = setInterval(
        () => this.tick(),1000
    );
}

tick(){
    this.setState({
        date: new Date()
    });
}
~~~

In coponentDidMount() method, we created a timer to call tick() every second. Then reset the date state. Once setState() method was called, it will automatically render component again. Thus, the component will be refreshed and update the date every second.

### 2. componentWillUnmount()

Inside this method, destroy the lifecycle resources used in component.

~~~
componentWillUnmount(){
    clearInterval(this.timerID);

}
~~~

### Works perfectly fine!

<img src="/assets/photos/React-lifecycle.png" style="width: 630px; margin: 0 auto; display:block;"/>
