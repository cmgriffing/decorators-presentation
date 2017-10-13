## A Basic Example (Class Method Decorator)

## Deprecated Class Method (usage)

```javascript
class WidgetUtilities {

  @deprecated
  makeWidget(widgetName, widgetType) {
    return {
      widgetName: widgetName.toLowerCase(),
      widgetType: widgetType.toLowerCase()
    }
  }

}

const widgetUtilities = new WidgetUtilities();
const newWidget = widgetUtilities.makeWidget('Widget A', 'foo');
// should print a warning to the console:
// 'Warning: WidgetUtilities.makeWidget is deprecated.'
```

<div class="notes">
Let us assume we have a library that other people will be using. We can't just remove the method yet, but we want to warn people that it will be going away sometime in the future.
</div>

## Deprecated Class Method (implementation)

```javascript

function deprecated(target, name, descriptor) {
  const oldMethod = descriptor.value;

  descriptor.value = function() {
  	console.warn(`Warning: ${target.constructor.name}.${name} is deprecated.`);
    oldMethod(...arguments);
  }.bind(target);
  
  return descriptor;
}

```

[-> Example in Typescript Playground](https://www.typescriptlang.org/play/#src=class%20WidgetUtilities%20%7B%0D%0A%0D%0A%20%20%40deprecated%0D%0A%20%20makeWidget(widgetName%2C%20widgetType)%20%7B%0D%0A%20%20%20%20return%20%7B%0D%0A%20%20%20%20%20%20widgetName%3A%20widgetName.toLowerCase()%2C%0D%0A%20%20%20%20%20%20widgetType%3A%20widgetType.toLowerCase()%0D%0A%20%20%20%20%7D%0D%0A%20%20%7D%0D%0A%0D%0A%7D%0D%0A%0D%0Aconst%20widgetUtilities%20%3D%20new%20WidgetUtilities()%3B%0D%0Aconst%20newWidget%20%3D%20widgetUtilities.makeWidget('Widget%20A'%2C%20'foo')%3B%0D%0A%0D%0Afunction%20deprecated(target%2C%20name%2C%20descriptor)%20%7B%0D%0A%20%20const%20oldMethod%20%3D%20descriptor.value%3B%0D%0A%0D%0A%20%20descriptor.value%20%3D%20function(...args)%20%7B%0D%0A%20%20%09console.warn(%60Warning%3A%20%24%7Btarget.constructor.name%7D.%24%7Bname%7D%20is%20deprecated.%60)%3B%0D%0A%20%20%20%20oldMethod(...args)%3B%0D%0A%20%20%7D.bind(target)%3B%0D%0A%20%20%0D%0A%20%20return%20descriptor%3B%0D%0A%7D)

## Deprecated Class Method (arguments usage)

What if we wanted to add a custom message?

```javascript
class WidgetUtilities {

  @deprecated('Please use `new Widget(widgetName, widgetType)` instead.')
  makeWidget(widgetName, widgetType) {
    return new Widget(widgetName, widgetType);
  }

}

const widgetUtilities = new WidgetUtilities();
const newWidget = widgetUtilities.makeWidget('Widget A', 'foo');
// should print a warning to the console:
// 'Warning: WidgetUtilities.makeWidget is deprecated. Please use `new Widget(widgetName, widgetType)` instead.'
```

<div class="notes">
In our previous example, we were using an object literal. But our new version of the library has a Widget class now.

We don't want to break code that relies on the makeWidget method existing. But we also want to let devs know that the Widget class exists.

Since decorators are just functions, we can pass arguments into them.
</div>

## Deprecated Class Method (arguments implementation)

```javascript

function deprecated(message) {

  return function(target, name, descriptor) {
    const oldMethod = descriptor.value;

    descriptor.value = function() {
      console.warn(`${target.constructor.name}.${name} is deprecated. ${message}`);
      oldMethod(...arguments);
    }.bind(target);
    
    return descriptor;
  }

}

```

<div class="notes">
Remember how we didn't use parentheses when calling deprecated earlier?

This is because the @ symbol handles calling the function with the required arguments.

This also means that we can use a higher order function to take in arguments and then return a function that has the signature that is expected.
</div>

## Stacking

```javascript
class WidgetUtilities {

  @deprecated()
  // measures the time it take to execute the method
  @time()
  makeWidget(widgetName, widgetType) {
    return {
      widgetName: widgetName.toLowerCase(),
      widgetType: widgetType.toLowerCase()
    }
  }

}

```

<div class="notes">

We can stack multiple decorators. The order sometimes matters though.

In this example, our timing function could be skewed in an unintended way if we are careless about the order.

</div>

## Stacking (contd.)


```javascript
// example a
class WidgetUtilities {

  makeWidget = deprecated( time( function(widgetName, widgetType) {
    return {
      widgetName: widgetName.toLowerCase(),
      widgetType: widgetType.toLowerCase()
    }
  }))

}

// example b
class WidgetUtilities {

  makeWidget = 
    deprecated(
      time(
        function(widgetName, widgetType) {
          return {
            widgetName: widgetName.toLowerCase(),
            widgetType: widgetType.toLowerCase()
          }
        }
      )
    )

}
```

<div class="notes">
You can think of the stacking in a similar way to this.

The implementations would be slightly different, but the end result would be the same.

As you can see, decorators are a little bit cleaner as you add more levels.
</div>

## Decorator Libraries

### Core Decorators
[https://github.com/jayphelps/core-decorators.js](https://github.com/jayphelps/core-decorators.js)

- inspired by languages that come with built-ins: @​override, @​deprecate, @​autobind, etc.

### Lodash-Decorators
[https://github.com/steelsojka/lodash-decorators](https://github.com/steelsojka/lodash-decorators)

- A collection of decorators using lodash at it's core. (@Memoize, @Debounce, @Throttle, etc.)

<div class="notes">

Just like lodash, you can import only what you need and avoid bloating your application.

It is important to note that these libraries still use the stage-0 spec implementation.

Core Decorators plans on updating once a compiler (Babel or TypeScript) implements the stage-2+ spec.

</div>

##

![](assets/good-dive.gif)

---
