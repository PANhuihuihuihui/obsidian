# TreeMap
All Implemented Interfaces:
Serializable, Cloneable, Map\<K,V\>, NavigableMap\<K,V\>, SortedMap\<K,V\>
- A Red-Black tree based NavigableMap implementation. The map is sorted according to the natural ordering of its keys, or by a Comparator provided at map creation time, depending on which constructor is used.
- O(logN) on  `containsKey`, `get`, `put` and `remove`
-  **is not synchronized**  Collections.synchronizedSortedMap

Related[[TreeMap]]