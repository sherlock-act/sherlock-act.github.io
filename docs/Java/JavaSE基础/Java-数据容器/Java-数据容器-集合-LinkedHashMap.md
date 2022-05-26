# Java-数据容器-集合-LinkedHashMap

- 哈希表和链表实现的`Map`接口，具有可预测的迭代次序。  这种实现不同于`HashMap，`它维持于所有条目的运行双向链表。  此链接列表定义迭代排序，通常是将键插入到Map（插入*顺序* ）中的顺序 。  
- LinkedHashMap的特点
  - 有序
  - 唯一
- LinkedHashMap的方法，其他方法继承自Map接口

| 方法名                                                       | 方法描述                                                     | 方法返回值类型      |
| ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------- |
| clear()                                                      | 从这张地图中删除所有的映射。                                 | void                |
| containsValue(Object value)                                  | 如果该地图将一个或多个键映射到指定的值，则返回 true 。       | boolean             |
| entrySet()                                                   | 返回此地图中包含的映射的Set视图。                            | Set<Map.Entry<K,V>> |
| forEach(BiConsumer<?  super K,? super V> action)             | 对此映射中的每个条目执行给定的操作，直到所有条目都被处理或操作引发异常。 | void                |
| get(Object key)                                              | 返回到指定键所映射的值，或 null如果此映射包含该键的映射。    | V                   |
| getOrDefault(Object key,  V defaultValue)                    | 返回到指定键所映射的值，或 defaultValue如果此映射包含该键的映射。 | V                   |
| keySet()                                                     | 返回此地图中包含的键的Set视图。                              | Set<K>              |
| removeEldestEntry(Map.Entry<K,V> eldest)                     | 如果此地图应删除其最老的条目，则返回 true 。                 | protected boolean   |
| replaceAll(BiFunction<?  super K,? super V,? extends V> function) | 将每个条目的值替换为对该条目调用给定函数的结果，直到所有条目都被处理或该函数抛出异常。 | void                |
| values()                                                     | 返回此地图中包含的值的Collection视图。                       | Collection<V>       |