---
layout: post
category : Delphi
tagline: "Supporting tagline"
tags : [Delphi]
---
{% include JB/setup %}

Assume there are two classes in a project, stand for two different layer. `THigherLayer` and `TLowerLayer`.

in `THigherLayer`, it calls a procedure in `TLowerLayer`, and inside this procedure, there may have some exceptions.

~~~
    Procedure THigherLayer.SomeProcedure;
    begin
      Some stuff;
      uLowerLayer.SomeProcedure(parameters);
    end;
~~~

And in `TLowerLayer`, we catched an exception

~~~
    Procedure TLowerLayer.SomeProcedure;
    begin
      try
        something;
      except
        on E:ErrorType do
          something;
        end;
      end;
    end;
~~~

The idea of adding a new event is to let higher layer handle the error and make actions for this error.

### Define an error handler in higher layer

`Procedure THigherLayer.EventHandler(Sender: TObject; SomeParameters; var Action);`, this will handle the error from lower layer, and then pass the Action value back to tell the lower layer what action need to be taken.

### Define the event in lower layer.

~~~
    TEvent = procedure(Sender: TObject; SomeParameters; var Action) of object;

    TLowerLayer = class
    private
      FOnEvent : TEvent;
    public
      property OnEvent : TEvent read FOnEvent write FOnEvent;
    end;
~~~

### Assign EventHandler to Event.

~~~
    THigherLayer.SomeProcedure;
    begin
      Some Stuff;
      LowerLayer.OnEvent := EventHandler;
    end;
~~~

### Raise event in lower layer.
~~~
    TLowerLayer.SomeProcedure;
    begin
      try
        some stuff;
      except
        on E:ErrorType do
          if Assigned(FOnEvent) then
            FOnEvent(self,SomeParameters,Action);
        end;
      end;
      Do some thing based on Action value;
    end;
~~~



