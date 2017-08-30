## Metadata

## What is metadata?

Metadata pertains to the code itself rather than the business logic.

eg:

- The name and type of the entity itself
- The name and type of each of its properties
- The name and type of its constructor arguments

## Spec/Shim

The Spec: [https://rbuckton.github.io/reflect-metadata/](https://rbuckton.github.io/reflect-metadata/)

The shim/repo: [https://github.com/rbuckton/reflect-metadata](https://github.com/rbuckton/reflect-metadata)

## General Usage (object or property)

```javascript
Reflect.defineMetadata(metadataKey, metadataValue, target);
Reflect.defineMetadata(metadataKey, metadataValue, target, propertyKey);

// check for presence of a metadata key on the prototype chain of an object or property
let result = Reflect.hasMetadata(metadataKey, target);
let result = Reflect.hasMetadata(metadataKey, target, propertyKey);
```

## Methods

```javascript
// define metadata on an object
Reflect.defineMetadata(metadataKey, metadataValue, target);

// check for presence of a metadata key on the prototype chain of an object
let result = Reflect.hasMetadata(metadataKey, target);

// check for presence of an own metadata key of an object
let result = Reflect.hasOwnMetadata(metadataKey, target);

// get metadata value of a metadata key on the prototype chain of an object
let result = Reflect.getMetadata(metadataKey, target);

// get metadata value of an own metadata key of an object
let result = Reflect.getOwnMetadata(metadataKey, target);

// get all metadata keys on the prototype chain of an object
let result = Reflect.getMetadataKeys(target);

// get all own metadata keys of an object
let result = Reflect.getOwnMetadataKeys(target);

// delete metadata from an object
let result = Reflect.deleteMetadata(metadataKey, target);
```

---
