# Java-数据容器-集合-HashMap

- 基于哈希表的实现的`Map`接口。  此实现提供了所有可选的`数据`操作，并允许`null`的值和`null`键。 （  `HashMap`类大致相当于`Hashtable` ，除了它是不同步的，并允许null）。这个类不能保证数据的顺序; 
- Map的特点
  - 无序
  - 唯一

- HashMap的方法

| 方法名                                                       | 方法解释                                                     | 方法返回值类型      |
| ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------- |
| clear()                                                      | 从这张地图中删除所有的映射。                                 | void                |
| clone()                                                      | 返回此 HashMap实例的浅拷贝：键和值本身不被克隆。             | Object              |
| compute(K key,  BiFunction<? super K,? super V,? extends V> remappingFunction) | 尝试计算用于指定键和其当前映射的值的映射（或 null如果没有当前映射）。 | V                   |
| computeIfAbsent(K key,  Function<? super K,? extends V> mappingFunction) | 如果指定的键尚未与值相关联（或映射到 null  ），则尝试使用给定的映射函数计算其值，并将其输入到此映射中，除非 null 。 | V                   |
| computeIfPresent(K key,  BiFunction<? super K,? super V,? extends V> remappingFunction) | 如果指定的密钥的值存在且非空，则尝试计算给定密钥及其当前映射值的新映射。 | V                   |
| containsKey(Object key)                                      | 如果此映射包含指定键的映射，则返回 true 。                   | boolean             |
| containsValue(Object value)                                  | 如果此地图将一个或多个键映射到指定值，则返回 true 。         | boolean             |
| entrySet()                                                   | 返回此地图中包含的映射的Set视图。                            | Set<Map.Entry<K,V>> |
| forEach(BiConsumer<?  super K,? super V> action)             | 对此映射中的每个条目执行给定的操作，直到所有条目都被处理或操作引发异常。 | void                |
| get(Object key)                                              | 返回到指定键所映射的值，或 null如果此映射包含该键的映射。    | V                   |
| getOrDefault(Object key,  V defaultValue)                    | 返回到指定键所映射的值，或 defaultValue如果此映射包含该键的映射。 | V                   |
| isEmpty()                                                    | 如果此地图不包含键值映射，则返回 true 。                     | boolean             |
| keySet()                                                     | 返回此地图中包含的键的Set视图。                              | Set<K>              |
| merge(K key,  V value, BiFunction<? super V,? super V,? extends  V> remappingFunction) | 如果指定的键尚未与值相关联或与null相关联，则将其与给定的非空值相关联。 | V                   |
| put(K key,  V value)                                         | 将指定的值与此映射中的指定键相关联。                         | V                   |
| putAll(Map<?  extends K,? extends V> m)                      | 将指定地图的所有映射复制到此地图。                           | void                |
| putIfAbsent(K key,  V value)                                 | 如果指定的键尚未与某个值相关联（或映射到 null ），则将其与给定值相关联并返回 null ，否则返回当前值。 | V                   |
| remove(Object key)                                           | 从该地图中删除指定键的映射（如果存在）。                     | V                   |
| remove(Object key,  Object value)                            | 仅当指定的密钥当前映射到指定的值时删除该条目。               | boolean             |
| replace(K key,  V value)                                     | 只有当目标映射到某个值时，才能替换指定键的条目。             | V                   |
| replace(K key,  V oldValue, V newValue)                      | 仅当当前映射到指定的值时，才能替换指定键的条目。             | boolean             |
| replaceAll(BiFunction<?  super K,? super V,? extends V> function) | 将每个条目的值替换为对该条目调用给定函数的结果，直到所有条目都被处理或该函数抛出异常。 | void                |
| size()                                                       | 返回此地图中键值映射的数量。                                 | int                 |
| values()                                                     | 返回此地图中包含的值的Collection视图。                       | Collection<V>       |