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

The **continue** statement is used to skip a specific iteration out of all the iterations. For example, consider the following code snippet:

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
