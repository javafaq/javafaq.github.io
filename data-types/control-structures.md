---
sort: 2
---

# Control Structures

Control structures are **statements** or **blocks** that are used to alter the execution flow of an application - depending on some condition. There are three types of control structures:

1. **Conditional Statements**: if, if-else, switch, ternary block.
2. **Loop Blocks**: for, while, do-while.
3. **Control Statements**: break, continue.

## Conditional Statements in java

The conditional statements are used to change the execution flow based on the validity of some condition. The **if** and **if-else** statements are used to define an execution path or an alternate flow depending on the validity of an underlying expression:

```java
private String weekEndOrWeekDay(String day){
    if(day.equals("Saturday") || day.equals("Sunday")){
        return "Weekend";
    }else{
        return "Weekday";
    }
}
```

**Switch** block is used to declutter the **if-else** block especially when the number of **if-else** statements is large. Implementing the same example as a **switch** block:

```java
private String weekEndOrWeekDay(String day){
    return switch(day){
        case "Saturday", "Sunday" -> "Weekend";
        default -> "Weekday";
    };
}
```

The **ternary expression** is the most tidy one out of all the conditional statements. But due to its nature, it becomes difficult to read if multiple conditions are nested one inside other.

```java
private String weekEndOrWeekDay(String day){
    return day.equals("Saturday") || day.equals("Sunday") ? "Weekend" : "Weekday";
}
```

## Loop blocks in java

There are three types of loops available in java - for, while and do-while. The loop blocks are used to repeatidly execute a block of statements controlled by some loop invariant (used to break the loop).

Consider the following examples to print first ten multiples of a number:

Using a **for** loop:

```java
private void firstTenMultiples(int number){
    // here i<=10 will break the loop after 10 iterations
    for(int i = 1; i <= 10; i++){
        System.out.println(number*i);
    }
}
```

Using a **while** loop:

```java
private void firstTenMultiples(int number){
    int index = 1;
    // here index <= 10 will break the loop after 10 iterations
    while(index <= 10){
        System.out.println(number* index);
        index++;
    }
}
```

Using a **do-while** loop:

```java
private static void firstTenMultiples(int number){
    int index = 1;
    do{
        System.out.println(number* index);
        index++;
    }
    // here index <=10 will break the loop after 10 iterations
    while(index<=10);
}
```

## Control Statements in java

The control statements - **break** and **continue** are used to alter the flow of a loop block. The **break** statement is used to early terminate a loop (instead of waiting for all the iterations to complete) for a perticular case:

```java
private static void firstFiveMultiples(int number){
    for(int i = 1; i <= 10; i++){
        if(number * i > 25){
            break;
        } else{
            System.out.println(number * i);
        }
    }
}
```

In the above example, we are using the same loop condition as mentioned above. But here we have added an additional check that will `break` the loop after 5 iterations for `i > 25`.

The **continue** statement is used to skip a specific iteration out of all the iterations. For example, consider the following code snippet. The `continue` statement for `i==25` will lead to the specific result being skipped from the output:

```java
private static void firstFiveMultiples(int number){
    for(int i = 1; i <= 10; i++){
        // this will skip the iteration with result = 25
        if(number * i == 25){
            continue;
        } else{
            System.out.println(number * i);
        }
    }
}
```

## Java enhanced for each loop

The enhanced `for` loop introduced in java5 allows us to iterate over arrays and collections without the need of explicitly declaring a loop variable.

```java
String[] fruits = new String[] { "Orange", "Mango", "Apple", "Grapes" };
for (String fruit : fruits) {
    System.out.println(fruit);
}
```

which is equivalent to:

```java
String[] fruits = new String[] { "Orange", "Mango", "Apple", "Grapes" };
for(int i = 0; i < fruits.length; i++){
    System.out.println(fruits[i]);
}
```

## Benefits of enhaned for loop

1. It promotes code readability.
2. It is more tidy as compared to traditional for loop construct.
3. It ensures that all the elements are traversed and avoids any unexpected results due to incorrect termination condition.

## Disadvantages of enhanced for loop

1. It cannnot be used to traverse the collection in reverse order.
2. It cannot be used to skip some elements (example, only process event or odd elements).

## Can we skip a break clause in switch block?

Yes, we can skip a `break` clause. But it will cause all the `case` blocks or `default` block to execute after first matching `case` block. Consider the following example:

```java
// assuming day = "Saturday"
private void weekEndOrWeekDay(String day){
    switch(day){
        case "Saturday", "Sunday" : {
            // this will be printed
            System.out.println("Weekend");
        }
        default: {
            // this will also be printed
            System.out.println("Weekday");
        }
    }
}
```

## Difference between dead code and unreachable code

The **dead code** is something that has no effect on the state of the program. For example, a few statements are executed but the results are not used:

```java
private void deadCode(int first, int second){
    int result = first + second;
}
```

Dead code is generally highlighted as a warning by the compiler.

On the other hand, **un-reachable** code - a compile time error denotes a flaw in the execution flow such that the code cannot be executed by following any path:

```java
private void deadCode(int first, int second){
    return;
    // compile time error; un-reachable code
    int result = first + second;
    System.out.println(result);
}
```
