## Another Basic Example (Class Method Decorator)

## Logging Method Arguments (usage)

```javascript
class WidgetMaker {

  @logArgs
  makeWidget(widgetName, widgetType) {
    // here for demonstration
  	console.log('original makeWidget');
    return {
      widgetName: widgetName.toLowerCase(),
      widgetType: widgetType.toLowerCase()
    }
  }

}

const widgetMaker = new WidgetMaker();
widgetMaker.makeWidget('Widget A', 'foo');
// logs: WidgetMaker.makeWidget called with args:, Widget A, foo
widgetMaker.makeWidget('Widget B', 'bar');
// logs: WidgetMaker.makeWidget called with args:, Widget B, bar
```

## Logging Method Arguments (decorator)

```javascript

function logArgs(target, name, descriptor) {

  console.log('target: ', target);
  // logs: Object { , 2 more… } 

  console.log('name: ', name);
  // logs: makeWidget

  console.log('descriptor: ', descriptor);
  // logs: undefined
  
  const oldMethod = target[name];
  target[name] = function() {

  	console.log(target.constructor.name + '.' + name + ' called with', arguments);

    oldMethod(...arguments);

  }.bind(target);
  
  return target;
}

```

---
