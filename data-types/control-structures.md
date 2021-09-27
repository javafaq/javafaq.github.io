---
sort: 2
---

# Control Structures

Control structures are **statements** or **blocks** that are used to alter the execution flow of an application - depending on some condition. There are three types of control structures:

1. **Conditional Statements**: if, if-else, switch, ternary block.
2. **Loop Blocks**: for, while, do-while.
3. **Control Statements**: break, continue.

## Explain various conditional statements and blocks in java

The conditional statements are used to change the execution flow based on the validity of some condition.

### if, if-else

The **if** and **if-else** statements are used to define an execution path or an alternate flow depending on the validity of an underlying expression:

```java
private String weekEndOrWeekDay(String day){
    if(day.equals("Saturday") || day.equals("Sunday")){
        return "Weekend";
    }else{
        return "Weekday";
    }
}
```

## switch block

**Switch** block is used to declutter the **if-else** block especially when the number of **if-else** statements is large. Implementing the same example as a **switch** block:

```java
private String weekEndOrWeekDay(String day){
    return switch(day){
        case "Saturday", "Sunday" -> "Weekend";
        default -> "Weekday";
    };
}
```

## Ternary expression

The ternary expression is the most tidy one out of all the conditional statements. But due to its nature, it becomes difficult to read if multiple conditions are nested one inside other.

```java
private String weekEndOrWeekDay(String day){
    return day.equals("Saturday") || day.equals("Sunday") ? "Weekend" : "Weekday";
}
```