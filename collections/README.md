---
sort: 3
---

# Collections

## Generics and Collections

1. Generics provides strong typesafety which ensures that the collections contain only a specefic type of elements. This reduces chances of `ClassCastException`.
2. The code becomes mroe readable and clean as we don't have to evaluate `instanceof` before performing any type speceifc operation.

## Common interfaces in collections framework

1. **[Iterable](https://docs.oracle.com/javase/8/docs/api/java/lang/Iterable.html)**: Allows the implementing class to be used with a `for-each` loop.
2. **[Collection](https://docs.oracle.com/javase/8/docs/api/java/util/Collection.html)**: The root interface of the collection hierarchy. This represents a collection of homogeneous elements.
3. **[List](https://docs.oracle.com/javase/8/docs/api/java/util/List.html)**: An ordered collection that allows **duplicates** as well.
4. **[Queue](https://docs.oracle.com/javase/8/docs/api/java/util/Queue.html)**: A collection of elements that can be accessed in **FIFO** order.
5. **[Set](https://docs.oracle.com/javase/8/docs/api/java/util/Set.html)**: A colelction of **unique** elements.
6. **[SortedSet](https://docs.oracle.com/javase/8/docs/api/java/util/SortedSet.html)**: A Set that further provides a total ordering on its elements. The elements are ordered using their natural ordering, or by a Comparator typically provided at sorted set creation time.
7. **[NavigableSet](https://docs.oracle.com/javase/8/docs/api/java/util/NavigableSet.html)**: A SortedSet extended with navigation methods reporting closest matches for given search targets. Methods lower, floor, ceiling, and higher return elements respectively less than, less than or equal, greater than or equal, and greater than a given element, returning null if there is no such element.

## Why Collection doesn’t extend Cloneable and Serializable interfaces?

Collection is a contract i.e. an abstraction to denote a group of elements. Support for **serialization** or **cloning** is something to be implemented in the actual implementation, as the higher level contract cannot have the actual object representation details - or the details required to decide whether serialization is even possible or not.

## What is an Iterator?

1. `Iterator` interface, implemented by the underlying collection on which `iterator()` method is called, provides methods to traverse a collection.
2. It supports removing elements from the underlying collection as well.
3. It promotes the **Iterator design pattern** allowing generic collection traversal irrespective of the actual collection type (ArrayList, LinkedList, HashSet, etc.)

## How Iterator is different from Enumeration?

1. Iterator is applicable to all Collection classes, whereas Enumeration is supported only for legacy classes like `Vector#elements()`.
2. To support legacy code, `Collections.enumeration(Collection<T> collection)` provides an option to generate an enumeration for other collection classes.
3. The `iterator()` method is inherited by the Collection classes from `Iterable` interface. No such inheritance applicable on `elements()` method.
4. Iterator supports additional methods like `remove()` to update the underlying collection during traversal. Enumerations on the other hand are read-only.

## Why there is no add() method in Iterator?

The newly added element could be added **out of the order** depending on the underlying collection and might work differently than expected.

## What is the difference between an Iterator and ListIterator?

1. `Iterator` can be used to traverse all the collection classes. `ListIterator` is specefic to the Lists only.
2. `ListIterator` can be used to travese the underlying list in either direction.
3. `ListIterator` support insertion of elements as well.

## What is fail-fast iteration?

1. The **fail-fast** iteration aborts the current iteration by throwing a `ConcurrentModificationException` as soon as a modification to the underlying collection is detected.
2. An instance field `modCount` is used to track the number of structural changes (add, remove elements) to the collection.
3. As soon as any un-expected changes to `modCount` are detected by the Iterator, `ConcurrentModificationException` is thrown to highlight the same.
4. Except for concurrent collections (`ConcurrentHashMap`, `CopyOnWriteArrayList`), all the `Iterable` classes support fail-fast iteration.

## What are different iteration strategies?

1. Fail Fast
2. Weakly Consistent
3. Snapshot

## What are Comparable and Comparator interface?

The `Comparable` interface allows any implementation class to provide default comparison strategy which is required for sorting and related operations. The strategy defined by `Comparable` is static and cannot be changed at runtime (for example inclusion of some additional attribute for comparsion).

The `Comparator` interface allows us to define a comparsion strategy that we can inject at runtime while performing various sorting operations. Consider the following example:

```java
List<String> fruits = Arrays.asList("Apple", "Orange", "Mango", "Banana");
Collections.sort(fruits); // [Apple, Banana, Mango, Orange]
Collections.sort(fruits, Collections.reverseOrder()); // [Orange, Mango, Banana, Apple]
```

## How to increase or decrease the capacity of ArrayList ?

1. `ensureCapacity(int)` : The capacity of an array list is automatically increased when we try to add more elements than the current capacity using the private `grow()` method. However, another utility method is provided to do it manually.
2. `trimToSize()` : used to trim the **capacity** of arrayList to the current **size** of ArrayList.

## How to get SubList from ArrayList ?

The `subList(from, to)` method from List interface can be used for generating a sublist from an original list.

## How HashSet eliminates duplicate values ?

1. `HashSet` internally uses `HashMap` for storing data, what it means is, when HashSet’s `add("E e")` method is called, add method internally calls `HashMap#put(key, value)` method with some **dummy** value (an `Object` instance named `PRESENT`).
2. Once `HashMap#put(key, value)` method is invoked, it stores the **data(key-value pair)** in bucket:
   1. By first evaluating hashcode of **key**
   2. Then identifies exact bucket
   3. and finally `equals` comparison of the **key** to store and the key of already stored key-value pairs in the list (if present).
   4. If **key** is already present, then it replaces the old value, with new value and returns old value.
   5. returns `null` otherwise

Depending on the response from the `HashMap#put(key, value)`, a `true` or `false` is returned denoting a duplicate entry.

## What is the significance of Collections.emptySet() over new HashSet<>()?

1. **Immutable** : The immutable result produced via `Collections.emptySet()` is inline with the intention of the programmer who wanted an empty set instead of a `null` value. A hashset generated using `new HashSet<>` can be populated with value which might not align with the context.
2. **Type Safety** : The type safety is ensured from the context without having to manually add generic type details.
3. **Reuse** : A singleton empty instance (ensured via immutability) is used wherever asked for. Thus this avoid crrreating unnecessary objects.
