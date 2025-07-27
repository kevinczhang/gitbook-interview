---
description: >-
  A Java Stream is a component that is capable of internal iteration of its
  elements, meaning it can iterate its elements itself.
---

# Stream

## **Stream Creation**

### By method of Stream.of

```java
Stream.of(arrayOfEmps[0], arrayOfEmps[1], arrayOfEmps[2]);
// OR
private static List<Employee> empList = Arrays.asList(arrayOfEmps);
empList.stream();
```

### &#x20;**Java 8 added a new&#x20;**_**stream()**_**&#x20;method to the&#x20;**_**Collection**_**&#x20;interface**

### By method of Stream.builder()

```java
Stream.Builder<Employee> empStreamBuilder = Stream.builder();

empStreamBuilder.accept(arrayOfEmps[0]);
empStreamBuilder.accept(arrayOfEmps[1]);

Stream<Employee> empStream = empStreamBuilder.build();
```

### Concatenate Streams

```java
Stream<String> concatStream = Stream.concat(stream1, stream2);
```

## Non-Terminal Operations

### map

```java
Stream<String> stringStream1 =
        stream.map((value) -> { return value.toLowerCase(); });
```

### filter

```java
Stream<String> longStringsStream = stream.filter((value) -> {
    return value.length() >= 3;
});
```

### distinct

```java
List<String> distinctStrings = stream
        .distinct()
        .collect(Collectors.toList());
```

### skip and limit

```java
Stream<Integer> infiniteStream = Stream.iterate(2, i -> i * 2);
List<Integer> collect = infiniteStream
    .skip(3)
    .limit(5)
    .collect(Collectors.toList());
assertEquals(collect, Arrays.asList(16, 32, 64, 128, 256));
```

### peek

```java
List<Employee> empList = Arrays.asList(arrayOfEmps);
    
empList.stream()
   .peek(e -> e.salaryIncrement(10.0))
   .peek(System.out::println)
   .collect(Collectors.toList());
```

