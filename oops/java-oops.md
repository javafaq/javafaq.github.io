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

An object is a runtime instance of a class. A class can thus be instantiated multiple times and all the resultant objects will be different each having their own state. The **state** of an object is defined by the current value of the class fields (if any).

The methods defined in a class when called on an object can be used to:

1. Alter the state of the object.
2. Access the state of the object.

```java
Employee john = new Employee("John", "Doe");
Employee jane = new Employee("Jane", "Doe");

john.getFirstName(); // access state
```

## What is inheritence in java?

The concept of **inheritence** allows an object to inherit state and behavior from another class promoting code reusability and modularization.