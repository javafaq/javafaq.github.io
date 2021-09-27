---
sort: 2
---

# Java OOPs

In this section, we will explore object oriented concepts in the context of java programming language.

## What is a class?

A class is a template that defines the data (attributes) and behaviors (the methods via which we can act upon the data). It acts as a blueprint for creating instances known as **Object**. Consider the following **example**:

```java
class Employee{
    private final String firstName;
    private final String lastName;

    public Employee(String fName, String lName){
        this.firstName = fName;
        this.lastName = lname;
    }

    public String getFirstName(){
        return this.firstName;
    }

    public String getLastName(){
        return this.lastName;
    }
}
```

The `Employee` class mentioned above contains two attributes **firstName** and **lastName** which are assigned a value via the **constructor** method. The two getter methods (getFirstName and getLastName) are used to access the corresponding values of the two attributes.

## What is an object?

An object is a runtime instance of a class. An object or instance of a class is created using a special method known as `constructor` method. If you have not provided a default constructor (non-parameterized constructor), the runtime environment creates one for you.

```tip
A constructor method cannot be marked as **final**. But we can have multiple constructors that vary in terms of the method signature.
```

A class can thus be instantiated multiple times and all the resultant objects will be different each having their own state. The **state** of an object is defined by the current value of the class fields (if any).

The methods defined in a class when called on an object can be used to:

1. Alter the state of the object.
2. Access the state of the object.

```java
Employee john = new Employee("John", "Doe");
Employee jane = new Employee("Jane", "Doe");

john.getFirstName(); // access state
```

## What is encapsulation in java?

It is the structure that couples the data (also known as state) and code that can modify the data into a single unit. In java, this is acheived using `class` as the unit of code.

To achieve encapsulation, the fields are given minimum visibility scope (ex: private) and the public methods are provided to access or update the fields. This allows us to put more control (if required) for field access or modification.

## What are the different types of methods in java?

1. **static methods**: These are not associated with any instance of the class and are called using the `ClassName.methodName` convention. Post java8, interfaces can also have static methods. In case of interface static methods, the implementation classes can call those using `InterfaceName.methodName` convention only.
   1. Static methods cannot access other **non-static** members directly.
   2. `this` and `super` are not available in static context.
   3. As these are associated with a class and not with any specific instance, these cannot be overridden.
2. **abstract methods**: A method marked with `abstract` keyword that does not have any body is termed as an abstract method. An abstract method can only be mentioned in an abstract class, but a class marked as abstract can have **zero-or-more** abstract methods.
3. **final methods**: A method marked as `final` can not be overridden by the child classes. This allows strict implementation contracts to be followed. This is actually the inverse of abstract methods.
4. **default methods**: Introduced in java8, an interface can have as many default methods without violating the contract with any of the implementation classes. In case of a class implementing multiple interfaces with same default method signature, the implementing class should explicitly specify which default method is to be used or it should override the default method.

```warning
Please note a difference between inherited static (class) methods and inherited non-static (instance) methods, that when you write a new static method with the same signature, the old static method is just hidden, not overridden.
```

## What is inheritence in java?

The concept of **inheritence** allows an object to inherit state and behavior from another class promoting code reusability and modularization. Consider the following example:

```java
class Calculator{
    int result;

    public int add(int first, int second){
        result = first + second;
        return result; // return first + second; should be used but assigning it to result for the sake of example
    }

    public int subtract(int first, int second){
        result = first - second;
        return result;
    }
}

class ExtendedCalculator extends Calculator{
    public int multiply(int first, int second){
        result = first * second; // result is inherited from parent Calculator
        return result;
    }
}

Calculator calculator = new Calculator();
ExtendedCalculator extendedCalculator = new ExtendedCalculator();

calculator.add(2,3); // 5
calculator.subtract(5,3); // 2
extendedCalculator.add(2,3) // 5 - inherited behavior
extendedCalculator.subtract(2,3) // -1 - inherited behavior
extendedCalculator.multiply(2,3) // 6
```

The `extendedCalculator` inherits both `add` and `subtract` methods from its parent class `Calculator`. It also inherits the `result` field from its parent. In addition to these, it has its own method `multiply`.

## What are the restrictions associated with inheritence in java?

Java inheritence follows the following rules:

1. Multiple inheritence is not supported i.e. a class cannot inherit from more than 1 class. This is to avoid **diamond problem**.
2. Private members (fields and methods) do NOT participate in inheritence. Any method in the child class with the same signature as of a private method in the parent class, is NOT overriding the parent class method as it was not even inherited from parent class.
3. Constructor(s) as well do NOT participate in inheritence. But when an instance of a child class is created, the parent constructor is automatically invoked so that the child instance can inherit appropriate state and behavior.
4. Cyclic inheritence is not allowed.

## What is polymorphism?

Used to provide different behaviors for the same type. Java provides two features to support this concept:

1. Method overloading - also known as compile time polymorphism or static or early binding.
2. Method overriding - also known as runtime polymorphism or dynamic or late binding.

```java
class Parent{
    public void callMe(){
        System.out.println("parent: callMe");
    }

    // overloaded method
    public void callMe(String args){
        System.out.println("parent: callMe with: " + args);
    }
}

class Child extends Parent{
    // overridden method
    public void callMe(){
        System.out.println("child: callMe");
        
    }
}

Parent p = new Parent();
Child c = new Child();

p.callMe(); // parent: callMe
p.callMe("hello"); // parent: callMe with: hello
c.callMe(); // child: callMe
c.callMe("world"); // parent: callMe with: world
```

`c.callMe("world")` resolves to the inherited overloaded method in the `Child` class.

## What is the difference between early vs late binding?

The code binding which can be decided at compile time (like fields and static members) is known as **early binding**. Example: method overloading.

On the other hand all other members are resolved at runtime via the actual object. This is known as **late binding** or runtime polymorphism. Example: method overriding.

Consider the following example:

```java
class Parent{
    public int test=10;
    public void instanceMethod(){
        System.out.println("parent: instanceMethod");
    }

    public static void staticMethod(){
        System.out.println("parent: staticMethod");
    }
}

class Child extends Parent{
    public int test=100;
    public void instanceMethod(){
        System.out.println("child: instanceMethod");
    }

    public static void staticMethod(){
        System.out.println("child: staticMethod");
    }
}

Parent parentReference = new Child();
Child childReference = new Child();
// late or runtime binding
parentReference.instanceMethod(); // child: instanceMethod
// early or static binding
parentReference.staticMethod(); // parent: staticMethod
// early or static binding
System.out.println(parentReference.test); //10
System.out.println(childReference.test); //100
```

Similar to static members, any non-static field members are also resolved at compile time and can't be overridden. If re-defined, the previous value is simply hidden.

## What is the difference between method hiding and overriding?

1. Method overriding is when a non-static method is re-defined in a child class and depending on the instance on which it is called, run-time polymorphism decides which definition is to be used (parent or child).
2. Method hiding is for static members that do not participate in inheritence (although available in child classes). When such methods are re-defined in child classes, the ones in the parent class are simply hidden.

Consider the following example:

```java
class Parent{
    public void instanceMethod(){
        System.out.println("parent: instanceMethod");
    }

    public static void staticMethod(){
        System.out.println("parent: staticMethod");
    }
}

class Child extends Parent{
    public void instanceMethod(){
        System.out.println("child: instanceMethod");
    }

    public static void staticMethod(){
        System.out.println("child: staticMethod");
    }
}

Parent parentReference = new Child();
Child childReference = new Child();

parentReference.instanceMethod(); // child: instanceMethod
parentReference.staticMethod(); // parent: staticMethod
childReference.instanceMethod(); // child: instanceMethod
childReference.staticMethod(); // child: staticMethod
```

You can check [this](https://coderanch.com/wiki/659959/Overriding-Hiding) page for more details.

## What are the different types of association between objects?

As java promotes code re-use, **association** is a way to achieve the same where objects use different types of relationships among them to achieve some goal. Following are the types of assocation:

1. **One to One**: A **Library** has **one** librarian.
2. **One to Many**: A **Library** has many **Books**.
3. **Many to One**: Many **books** are housed in a **library**.
4. **Many to Many**: Many **books** can have multiple **authors**.

## How do we achieve association?

Association is the way multiple java objects interact with each other. We can achieve the same using either of the following methods:

- **Aggregation**: It represents a **has-a** relationship where an object contains a reference to other object which can exist independently as well.
- **Composition**: It represents a **part-of** relationshiop where an object is part of the state of other object and cannot exist independently.

```tip
**Composition** represents a stronger association as compared to **aggregation**.
```
