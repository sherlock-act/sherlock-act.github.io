# Java-数据容器-集合-Map

- Map存储数据的方式都是一对一对的进行存储，例如：{lulu=345678, nana=789654, xiaoli=654321}
- Map的特点
  - 无序
  - 唯一
- Map的方法

|                           方法名称                           |                         方法详细描述                         |   方法返回值类型    |
| :----------------------------------------------------------: | :----------------------------------------------------------: | :-----------------: |
|                         ==clear()==                          |            从该地图中删除所有的映射（可选操作）。            |        void         |
| compute(K key,  BiFunction<? super K,? super V,? extends V> remappingFunction) | 尝试计算指定键的映射及其当前映射的值（如果没有当前映射， null ）。 |      default V      |
| computeIfAbsent(K key,  Function<? super K,? extends V> mappingFunction) | 如果指定的键尚未与值相关联（或映射到 null  ），则尝试使用给定的映射函数计算其值，并将其输入到此映射中，除非 null 。 |      default V      |
| computeIfPresent(K key,  BiFunction<? super K,? super V,? extends V> remappingFunction) | 如果指定的密钥的值存在且非空，则尝试计算给定密钥及其当前映射值的新映射。 |      default V      |
|                 ==containsKey(Object key)==                  |          如果此映射包含指定键的映射，则返回 true 。          |       boolean       |
|               ==containsValue(Object value)==                |    如果此地图将一个或多个键映射到指定的值，则返回 true 。    |       boolean       |
|                        ==entrySet()==                        |              返回此地图中包含的映射的Set视图。               | Set<Map.Entry<K,V>> |
|                     ==equals(Object o)==                     |          将指定的对象与此映射进行比较以获得相等性。          |       boolean       |
|       forEach(BiConsumer<?  super K,? super V> action)       | 对此映射中的每个条目执行给定的操作，直到所有条目都被处理或操作引发异常。 |    default void     |
|                     ==get(Object key)==                      |  返回到指定键所映射的值，或 null如果此映射包含该键的映射。   |          V          |
|          getOrDefault(Object key,  V defaultValue)           | 返回到指定键所映射的值，或 defaultValue如果此映射包含该键的映射。 |      default V      |
|                          hashCode()                          |                    返回此地图的哈希码值。                    |         int         |
|                        ==isEmpty()==                         |           如果此地图不包含键值映射，则返回 true 。           |       boolean       |
|                         ==keySet()==                         |               返回此地图中包含的键的Set视图。                |       Set<K>        |
| merge(K key,  V value, BiFunction<? super V,? super V,? extends  V> remappingFunction) | 如果指定的键尚未与值相关联或与null相关联，则将其与给定的非空值相关联。 |      default V      |
|                   ==put(K key,  V value)==                   |       将指定的值与该映射中的指定键相关联（可选操作）。       |          V          |
|           putAll(Map<?  extends K,? extends V> m)            |        将指定地图的所有映射复制到此映射（可选操作）。        |        void         |
|                 putIfAbsent(K key,  V value)                 | 如果指定的键尚未与某个值相关联（或映射到 null ）将其与给定值相关联并返回 null ，否则返回当前值。 |      default V      |
|                    ==remove(Object key)==                    |    如果存在（从可选的操作），从该地图中删除一个键的映射。    |          V          |
|            ==remove(Object key,  Object value)==             |        仅当指定的密钥当前映射到指定的值时删除该条目。        |   default boolean   |
|                   replace(K key,  V value)                   |       只有当目标映射到某个值时，才能替换指定键的条目。       |      default V      |
|           replace(K key,  V oldValue, V newValue)            |       仅当当前映射到指定的值时，才能替换指定键的条目。       |   default boolean   |
| replaceAll(BiFunction<?  super K,? super V,? extends V> function) | 将每个条目的值替换为对该条目调用给定函数的结果，直到所有条目都被处理或该函数抛出异常。 |    default void     |
|                          ==size()==                          |                 返回此地图中键值映射的数量。                 |         int         |
|                         ==values()==                         |            返回此地图中包含的值的Collection视图。            |    Collection<V>    |

