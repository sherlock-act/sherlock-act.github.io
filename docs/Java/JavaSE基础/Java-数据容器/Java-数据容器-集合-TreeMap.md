# Java-数据容器-集合-TreeMap

- 一个红黑树基于NavigableMap实现。  该地图是根据排序natural ordering其密钥，或通过Comparator在地图创建时提供，这取决于所使用的构造方法。  

- TreeMap的特点
  - 相对有序（基于二叉树排序）
  - 唯一

- TreeMap的其他方法

| 方法名                                                       | 方法描述                                                     | 方法返回值类型        |
| ------------------------------------------------------------ | ------------------------------------------------------------ | --------------------- |
| ceilingEntry(K key)                                          | 返回与大于或等于给定键的最小键相关联的键值映射，如果没有此键，则  null 。 | Map.Entry<K,V>        |
| ceilingKey(K key)                                            | 返回大于或等于给定键的 null键，如果没有此键，则返回 null 。  | K                     |
| clear()                                                      | 从这张地图中删除所有的映射。                                 | void                  |
| clone()                                                      | 返回此 TreeMap实例的浅拷贝。                                 | Object                |
| comparator()                                                 | 返回用于订购此地图中的键的比较器，或null如果此地图使用其键的natural ordering 。 | Comparator<? super K> |
| containsKey(Object key)                                      | 如果此映射包含指定键的映射，则返回 true 。                   | boolean               |
| containsValue(Object value)                                  | 如果此地图将一个或多个键映射到指定值，则返回 true 。         | boolean               |
| descendingKeySet()                                           | 返回此地图中包含的键的相反顺序NavigableSet 。                | NavigableSet<K>       |
| descendingMap()                                              | 返回此映射中包含的映射的反向排序视图。                       | NavigableMap<K,V>     |
| entrySet()                                                   | 返回此地图中包含的映射的Set视图。                            | Set<Map.Entry<K,V>>   |
| firstEntry()                                                 | 返回与该地图中的最小键相关联的键值映射，如果地图为空，则返回 null 。 | Map.Entry<K,V>        |
| firstKey()                                                   | 返回此地图中当前的第一个（最低）键。                         | K                     |
| floorEntry(K key)                                            | 返回与小于或等于给定键的最大键相关联的键值映射，如果没有此键，则  null 。 | Map.Entry<K,V>        |
| floorKey(K key)                                              | 返回小于或等于给定键的最大键，如果没有这样的键，则返回 null 。 | K                     |
| forEach(BiConsumer<?  super K,? super V> action)             | 对此映射中的每个条目执行给定的操作，直到所有条目都被处理或操作引发异常。 | void                  |
| get(Object key)                                              | 返回到指定键所映射的值，或 null如果此映射包含该键的映射。    | V                     |
| headMap(K toKey)                                             | 返回此地图部分的视图，其密钥严格小于 toKey 。                | SortedMap<K,V>        |
| headMap(K toKey,  boolean inclusive)                         | 返回此地图部分的视图，其键值小于（或等于，如果 inclusive为真） toKey 。 | NavigableMap<K,V>     |
| higherEntry(K key)                                           | 返回与最小密钥相关联的密钥值映射严格大于给定密钥，如果没有这样的密钥则  null 。 | Map.Entry<K,V>        |
| higherKey(K key)                                             | 返回严格大于给定键的最小键，如果没有这样的键，则返回 null 。 | K                     |
| keySet()                                                     | 返回此地图中包含的键的Set视图。                              | Set<K>                |
| lastEntry()                                                  | 返回与该地图中最大关键字关联的键值映射，如果地图为空，则返回 null 。 | Map.Entry<K,V>        |
| lastKey()                                                    | 返回当前在此地图中的最后（最高）键。                         | K                     |
| lowerEntry(K key)                                            | 返回与最大密钥相关联的密钥值映射严格小于给定密钥，如果没有这样的密钥，则  null 。 | Map.Entry<K,V>        |
| lowerKey(K key)                                              | 返回严格小于给定键的最大键，如果没有这样的键，则返回 null 。 | K                     |
| navigableKeySet()                                            | 返回此地图中包含的键的NavigableSet视图。                     | NavigableSet<K>       |
| pollFirstEntry()                                             | 删除并返回与该地图中的最小键相关联的键值映射，如果地图为空，则返回  null 。 | Map.Entry<K,V>        |
| pollLastEntry()                                              | 删除并返回与该地图中最大密钥相关联的键值映射，如果地图为空，则返回  null 。 | Map.Entry<K,V>        |
| put(K key,  V value)                                         | 将指定的值与此映射中的指定键相关联。                         | V                     |
| putAll(Map<?  extends K,? extends V> map)                    | 将指定地图的所有映射复制到此地图。                           | void                  |
| remove(Object key)                                           | 从此TreeMap中删除此键的映射（如果存在）。                    | V                     |
| replace(K key,  V value)                                     | 只有当目标映射到某个值时，才能替换指定键的条目。             | V                     |
| replace(K key,  V oldValue, V newValue)                      | 仅当当前映射到指定的值时，才能替换指定键的条目。             | boolean               |
| replaceAll(BiFunction<?  super K,? super V,? extends V> function) | 将每个条目的值替换为对该条目调用给定函数的结果，直到所有条目都被处理或该函数抛出异常。 | void                  |
| size()                                                       | 返回此地图中键值映射的数量。                                 | int                   |
| subMap(K fromKey,  boolean fromInclusive, K toKey, boolean toInclusive) | 返回此地图部分的视图，其关键范围为 fromKey至 toKey 。        | NavigableMap<K,V>     |
| subMap(K fromKey,  K toKey)                                  | 返回此地图部分的视图，其关键字范围从 fromKey （含）到 toKey ，独占。 | SortedMap<K,V>        |
| tailMap(K fromKey)                                           | 返回此地图部分的视图，其键大于等于 fromKey 。                | SortedMap<K,V>        |
| tailMap(K fromKey,  boolean inclusive)                       | 返回此地图部分的视图，其键大于（或等于，如果 inclusive为真） fromKey 。 | NavigableMap<K,V>     |
| values()                                                     | 返回此地图中包含的值的Collection视图。                       | Collection<V>         |