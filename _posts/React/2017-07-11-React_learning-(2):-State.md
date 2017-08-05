---
layout: post
category : ReactJS
tagline: "Supporting tagline"
tags : [ReactJS,Frontend]
---
{% include JB/setup %}

Today I am gonna to learn 'state' in React.

As we know from befor, "props" in React accepts arbitrary inputs, it is const since we get the value.    

State in React allows us to change component "reactly" or dynamically. 

### Adding State to Class

*  Add a class constructor to assign the initial state value

~~~
constructor(props){
    super(props);
    this.state = {
        color: "pink"
    };
}
~~~

Class components should always call the base constructor with `props`.

* Add state component in `<div>` class

~~~
    render(){
        const styleObj = {
            backgroundColor: this.state.color
        };

        return(
            <div style={styleObj} >
                <h1>Hello World!</h1>
                <h2>{this.props.name}</h2>
            </div>
        );
    }
~~~

This will set the `<div>` background color to the color value in `state`.

Now if we test the page ,it will show like this.

<img src="/assets/photos/React-state-1.png" alt="1" style="width: 630px; margin: 0 auto; display:block;"/>

### Dynamically change state

As we said before, state is used for dynamically self changed to react. How would that achieved?

`this.setState({})` is a function used to reset the state value, thus it could be used to reset the `color` value.

* Add function to change state.

~~~
    toogleColor(){
        if(this.state.color === "pink"){
            this.setState({
                color: "yellow"
            });
        } else {
            this.setState({
                color: "pink"
            });
        }
    }
~~~

`toogleColor()` will change color in `state` between 'pink' and 'yellow'.    
Don't forget to add binding in constructor to make `this` work in callback.
~~~
    constructor(props){
        super(props);
        this.state = {
            color: "pink"
        };
        this.toogleColor = this.toogleColor.bind(this);
    }
~~~

* Link toggleColor() with a button.

~~~
    render(){
        const styleObj = {
            backgroundColor: this.state.color
        };

        return(
            <div style={styleObj} >
                <h1>Hello World!</h1>
                <h2>{this.props.name}</h2>
                <button onClick={this.toogleColor}>ToggleColor</button>
            </div>
        );
    }
~~~

Now when we click the 'ToggleColor' button, the background color will change.

<img src="/assets/photos/React-state-2.png" alt="2" style="width: 630px; margin: 0 auto; display:block;"/>

Click it!

<img src="/assets/photos/React-state-3.png" alt="3" style="width: 630px; margin: 0 auto; display:block;"/>


Demo Code in Github: [https://github.com/cxx7532706/ReactLearn](https://github.com/cxx7532706/ReactLearn)
