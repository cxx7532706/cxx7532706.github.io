---
layout: post
category : Delphi
tagline: "Supporting tagline"
tags : [Delphi]
---
{% include JB/setup %}

### Why would we use Class Reference?

For example, if we have a base class 'TCar', and two different color cars 'TRedCar' and 'TBlueCar'.

We need to determine which kind of car we want to create a instance for, normally what we did is
~~~
CarType := Input.CarType;
CarCreate(Parameter1, Parameter2, ..., CarType);
~~~
And inside of CarCreate(), we do `if` or `switch` logic to create different instance based on `CarType`.

However with class reference, we could write a same code for all differente subClass creation.

### How?

By using `TCarClass = class of TCar`, this declared a class reference, it can be assigned value by `TCar` or `TRedCar` `TBlueCar`, it represents an class.

~~~
if CarType = 'Red' then
  TCarClass := TRedCar
else if CarType = 'Blue' then
  TCarClass := TBlueCar;
CarCreate(Parameters, ..., TCarClass);
~~~

Then in `CarCreate()` procedure, all you need to do is `Car := TCarClass.Create(Parameters);`

This will automatically call different constructor based on different classes.

Doesn't need any other `if` or `switch` anymore!
