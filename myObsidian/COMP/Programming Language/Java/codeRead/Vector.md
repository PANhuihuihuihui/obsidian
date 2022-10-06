# Vector
All Implemented Interfaces:
Serializable, Cloneable, Iterable\<E\>, Collection\<E\>, List\<E\>, RandomAccess
- grow or shrink as needed 一般只是稍大一点。如果需要添加很多，可以自己increse a large size 来减少relocation 的时间消耗
- `Vector` is synchronized if not need sychronized ArrayList is better.
- fast-failed