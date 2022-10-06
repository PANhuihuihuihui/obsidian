# HashSet
All Implemented Interfaces: Serializable, Cloneable, Iterable\<E\>, Collection\<E\>, Set\<E\>
- This class implements the Set interface, backed by a hash table (actually a **HashMap instance**).
- no guarantees about the order in literation 
- permits the null element
- O(1) `add`, `remove`, `contains` and `size`  O(N+C): Iterating ? 到底是为什么
- **not synchronized.** Collections.synchronizedSet(new HashSet(...))
- _fail-fast_ 