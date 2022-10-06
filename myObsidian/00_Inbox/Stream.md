### Function

### Diffference
map() and flatmap():= for nested structure
```java
List<String> myList = Stream.of("a", "b") .map(String::toUpperCase) .collect(Collectors.toList()); assertEquals(asList("A", "B"), myList);
// works well
List<List<String>> list = Arrays.asList( Arrays.asList("a"), Arrays.asList("b")); System.out.println(list);
//_[[a], [b]]_.
System.out.println(list .stream() .flatMap(Collection::stream) .collect(Collectors.toList()));
// works well
```
