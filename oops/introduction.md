---
sort: 1
---

# Introduction

## What is Object oriented programming?

**Object oriented programming** is a methodology where the individual re-usable components known as **classes** are created to work together for achieveing the overall software application purpose. The clases together with the runtime instances (known as **objects**) provide a way to structure a software application as small manageable units.

## What is a class?

A class is a template that defines the data (attributes) and behaviors (the methods via which we can act upon the data). It acts as a blueprint for creating instances known as **Object**.

## What is an object?

An object is a runtime instance of a class. A class can thus be instantiated multiple times and all the resultant objects will be different each having their own state.

```warning
The term **object** is used to define a runtime instance of a class which is different than the class `java.lang.Object` which acts as a parent to all the instances in java.
```

## What are the features of OOPs?

- **Encapsulation**: self contained modules that bind the data and the methods that can process the data.
- **Abstraction**: is the techqniue of hiding details via visibility scope using **public**, **protected**, **private**, **default** modifiers. It allows the developers to expose only high level details, keeping the low level implementation details private.
- **Inheritence**: allows the arrangement of components(classes, interface, etc.) in hierarchical order which result in sharing of data and behaviour from parent to child classes. This promotes reusing the existing components by extending and creating child components.
- **Polymorphism**: it litteraly means "many forms". Using polymorphism, we can define one contract (say an interface method) and can provide its multiple implementations which can be resolved at runtime depending on the obejct being used.

```tip
**Abstraction** hides the implementation details whereas **Encapsulation** wraps code and data into a single unit.
```
