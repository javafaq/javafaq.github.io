---
sort: 1
---

# Data Types

## What is a data type?

The data type determines the value that can be stored in a variable. It provides details about the type and the size of data that the reference variable can hold.

There are two types of data types in java programming language:

1. **Primitive**: The 8 pre-defined data types (boolean, char, byte, short, int, long, float and double).
2. **User Defined**: These are non-primitive types such as Classes, interface and arrays.

## What is the size and default value of various primitive types in java?

The following is the details of various primitive data types:

|   Type                                         | Bits | Bytes |   Min         |    Max          | Default |
|:----------------------------------------------:|:----:|:-----:|:-------------:|:---------------:|:-------:|
| byte                                           | 8    | 1     | $$-2^{8-1}$$  | $$2^{8-1} -1$$  | 0       |
| short                                          | 16   | 2     | $$-2^{16-1}$$ | $$2^{16-1} -1$$ | 0       |
| int                                            | 32   | 4     | $$-2^{32-1}$$ | $$2^{32-1} -1$$ | 0       |
| long                                           | 64   | 8     | $$-2^{64-1}$$ | $$2^{64-1} -1$$ | 0       |
| float                                          | 32   | 4     | NA            | NA              | 0.0f    |
| double                                         | 64   | 8     | NA            | NA              | 0.0d    |
| boolean                                        | 1    | NA    | NA            | NA              | false   |
| [char](https://stackoverflow.com/a/5078365)    | 16   | 2     | NA            | NA              | ''      |

## What are wrapper classes?

A wrapper class is a class that acts as a container for a primitive data type. The primary objective of using wrapper classes is to wrap primitive values as java objects so that those can be used where primitive types are not allowed like `ArrayList` data structure of **generics**.

## What is autoboxing and unboxing?

The automatic wrapping of a primitive type to its wrapper class is known as autoboxing. On the other hand, unboxing is the opposite of this where a wrapper class is automatically converted to a primitive type. Consider the following example:

```java
class AutoboxingUnboxingExample {
    public static void main(String[] args) {
        AutoboxingUnboxingExample auex = new AutoboxingUnboxingExample();
        //autoboxing of 5 as the args in method autoBoxingExample is a wrapper type
        int result = auex.autoBoxingExample(5);
    }

    // autoboxing
    public int autoBoxingExample(Integer input) {
        return input * 2; // unboxing of input to primitive type
    }

}
```

## What are the various scopes of existence for primitive variables?

1. **Class or static fields**: Loaded as part of the class loading process. These continue to exist until the class is unloaded from the memory.
2. **Instance or non-static fields**: Associated with the state of a specific object, these cease to exist as soon as the corresponding object is garbage collected.
3. **Local variables**: These co-exist with the scope of the method in which these are defined. As soon as the method is offloaded from the stack, these variables are also destroyed.
4. **Block variables**: These have the shortest lifespan limited only to the block in which these are defined like a for loop or if block.

## What do we mean by pass by value or reference?

Both of these terms are used in the context of how formal and actual parameters are resolved during a method call.

In call by value, values of actual parameters are copied to method's formal parameters and the two types of parameters are stored in different memory locations. But in case of call by reference, both formal and actual arguments point to the same memory location.

```tip
Java is always **pass by value**. It also passes references to objects by value. Refer to [this](https://stackoverflow.com/questions/40480/is-java-pass-by-reference-or-pass-by-value) link for more details.
```

## What is type casting?

It helps us to assign value of a given type to variable of another type. Casting is applicable to both primitive and non-primitive data types.

In case of primitive data types, this might lead to loss of information depending on the allowed value range:

```java
int integerValue  = 32767;
short shortValue;
shortValue = (short) integerValue; // casting

System.out.println(integerValue); // 32727
System.out.println(shortValue); // 32767

// update the integer value to cross the short range
int integerValue  = 32768;
short shortValue;
shortValue = (short) integerValue;

System.out.println(integerValue); // 32768
System.out.println(shortValue); // -32768
```

In case of object type casting, the allowed methods are of the target type:

```java
String name = "JAVA FAQ";
System.out.println(name.toLowerCase()); // java faq

Object castedName = (Object) name;
// methods from Object class available on castedName; no method from String class available here
System.out.println(castedName.hashCode()); // some hashcode is printed 
```

## Arrays vs Collection Classes?

1. Collections support generic types for strict compile time checks whereas Arrays do not support the same.
2. Arrays are of fixed size whereas collection classes can grow dynamically.
3. Arrays can store both primtive as well as non-primitive (Objects) types whereas collection classes only support non-primitive types.
4. Collection classes provide a lot of utility methods to manipulate the underlying data structure.
5. Depending on the underlyinng data structure, the data in a collection can be stored lineraly or non-lineraly whereas arrays only support linear data storage.
