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
  const oldMethod = target[name];

  target[name] = function() {
  	console.warn(`Warning: ${target.constructor.name}.${name} is deprecated.`);
    oldMethod(...arguments);
  }.bind(target);
  
  return target;
}

```

## Deprecated Class Method (arguments usage)

What if we wanted to add a custom message?

In this case, we want to let the user know about creating the widget using the Widget class.

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
    const oldMethod = target[name];

    target[name] = function() {
      console.warn(`${target.constructor.name}.${name} is deprecated. ${message}`);
      oldMethod(...arguments);
    }.bind(target);
    
    return target;
  }

}

```

<div class="notes">
Remember how we didn't use parentheses when calling deprecated earlier?

This is because the @ symbol handles calling the function with the required arguments.

This also means that we can use a higher order function to take in arguments and then return a function that has the signature that is expected.
</div>

---
