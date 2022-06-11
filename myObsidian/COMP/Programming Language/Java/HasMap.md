# HasMap
## Defination
- HashMap 是一个**散列表**，它存储的内容是键值对(key-value)映射。
- HashMap 实现了 Map 接口，根据键的 HashCode 值存储数据，具有很快的访问速度，最多允许一条记录的键为 null，**不支持线程同步**。
- HashMap 是**无序的**，即不会记录插入的顺序。
- HashMap **继承于AbstractMap**，实现了 **Map、Cloneable、java.io.Serializable 接口**。
- HashMap 的 key 与 value 类型可以相同也可以不同
- HashMap 中的元素实际上是对象，一些常见的基本类型可以使用它的包装类

## Example
```java
 import java.util.HashMap; // 引入 HashMap 类
 HashMap<Integer, String> Sites = new HashMap<Integer, String>();
 Sites.put(1, "Google");  
 Sites.put(2, "Runoob");
 Sites.put(3, "Taobao");  
 Sites.put(4, "Zhihu");
 //{1=Google, 2=Runoob, 3=Taobao, 4=Zhihu}
 Sites.get(3);
 // Taobao
 Sites.remove(4);
 //{1=Google, 2=Runoob, 3=Taobao}
 Sites.clear();
 Sites.size();
 // 输出 key 和 value
 for (Integer i : Sites.keySet()) {  
	System.out.println("key: " + i + " value: " + Sites.get(i));  
 }  
// 返回所有 value 值  
 for(String value: Sites.values()) {  
  // 输出每一个value  
  System.out.print(value + ", ");  
  }

```
## Method
方法

描述

[clear()](https://www.runoob.com/java/java-hashmap-clear.html)

删除 hashMap 中的所有键/值对

[clone()](https://www.runoob.com/java/java-hashmap-clone.html)

复制一份 hashMap

[isEmpty()](https://www.runoob.com/java/java-hashmap-isempty.html)

判断 hashMap 是否为空

[size()](https://www.runoob.com/java/java-hashmap-size.html)

计算 hashMap 中键/值对的数量

[put()](https://www.runoob.com/java/java-hashmap-put.html)

将键/值对添加到 hashMap 中

[putAll()](https://www.runoob.com/java/java-hashmap-putall.html)

将所有键/值对添加到 hashMap 中

[putIfAbsent()](https://www.runoob.com/java/java-hashmap-putifabsent.html)

如果 hashMap 中不存在指定的键，则将指定的键/值对插入到 hashMap 中。

[remove()](https://www.runoob.com/java/java-hashmap-remove.html)

删除 hashMap 中指定键 key 的映射关系

[containsKey()](https://www.runoob.com/java/java-hashmap-containskey.html)

检查 hashMap 中是否存在指定的 key 对应的映射关系。

[containsValue()](https://www.runoob.com/java/java-hashmap-containsvalue.html)

检查 hashMap 中是否存在指定的 value 对应的映射关系。

[replace()](https://www.runoob.com/java/java-hashmap-replace.html)

替换 hashMap 中是指定的 key 对应的 value。

[replaceAll()](https://www.runoob.com/java/java-hashmap-replaceall.html)

将 hashMap 中的所有映射关系替换成给定的函数所执行的结果。

[get()](https://www.runoob.com/java/java-hashmap-get.html)

获取指定 key 对应对 value

[getOrDefault()](https://www.runoob.com/java/java-hashmap-getordefault.html)

获取指定 key 对应对 value，如果找不到 key ，则返回设置的默认值

[forEach()](https://www.runoob.com/java/java-hashmap-foreach.html)

对 hashMap 中的每个映射执行指定的操作。

[entrySet()](https://www.runoob.com/java/java-hashmap-entryset.html)

返回 hashMap 中所有映射项的集合集合视图。

[keySet](https://www.runoob.com/java/java-hashmap-keyset.html)()

返回 hashMap 中所有 key 组成的集合视图。

[values()](https://www.runoob.com/java/java-hashmap-values.html)

返回 hashMap 中存在的所有 value 值。

[merge()](https://www.runoob.com/java/java-hashmap-merge.html)

添加键值对到 hashMap 中

[compute()](https://www.runoob.com/java/java-hashmap-compute.html)

对 hashMap 中指定 key 的值进行重新计算

[computeIfAbsent()](https://www.runoob.com/java/java-hashmap-computeifabsent.html)

对 hashMap 中指定 key 的值进行重新计算，如果不存在这个 key，则添加到 hasMap 中

[computeIfPresent()](https://www.runoob.com/java/java-hashmap-computeifpresent.html)

对 hashMap 中指定 key 的值进行重新计算，前提是该 key 存在于 hashMap 中。