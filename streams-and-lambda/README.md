---
sort: 6
---

# Streams and Lambda Expressions

With the introduction of **streams**, java8 provided support for functional style of programming which was previously common in procedural programming languages.

```warning
A stream should not be confused with a type or data structure. It simply represents a flow of elements from the underlying data structure like an `ArrayList`.
```

1. Various methods (like map, filter, count, etc.) can be chained together to form a pipeline to process a stream of elements consumed from any underlying data structure.
2. A stream does not alter the underlying collection.
3. Various stream operations can be categorized as:
   1. **Intermediatry**: These are lazily executed. Example: `map`
   2. **Terminal**: These are used to mark the end of a stream pipeline and return result on execution. Example: `collect`

## Some common operations

### How to prepare a frequency map from an int array?

```java
public Map<Integer, Long> calculateFrequency(int[] nums){
    return Arrays.stream(nums).boxed().collect(Collectors.groupingBy(Function.identity(), Collectors.counting()));
}
```
