# Java-数据容器-集合-Collection

- List接口与Set接口都继承自Collection
- 继承自Collection的接口或实现类，存储数据的方式都是一个一个的存储的。
- Collection的遍历方式
  - 增强for循环
  - 迭代器：iterator()
- Collection的方法，常用方法黄字标底

|                方法名称                |                         方法详细描述                         |     方法返回值类型     |
| :------------------------------------: | :----------------------------------------------------------: | :--------------------: |
|              ==add(E e)==              |            确保此集合包含指定的元素（可选操作）。            |        boolean         |
|   addAll(Collection<?  extends E> c)   |       将指定集合中的所有元素添加到此集合（可选操作）。       |        boolean         |
|              ==clear()==               |             从此集合中删除所有元素（可选操作）。             |          void          |
|         ==contains(Object o)==         |           如果此集合包含指定的元素，则返回 true 。           |        boolean         |
|      containsAll(Collection<?> c)      |      如果此集合包含指定 集合中的所有元素，则返回true。       |        boolean         |
|          ==equals(Object o)==          |          将指定的对象与此集合进行比较以获得相等性。          |        boolean         |
|               hashCode()               |                    返回此集合的哈希码值。                    |          int           |
|             ==isEmpty()==              |             如果此集合不包含元素，则返回 true 。             |        boolean         |
|             ==iterator()==             |                 返回此集合中的元素的迭代器。                 |      Iterator<E>       |
|            parallelStream()            |          返回可能并行的 Stream与此集合作为其来源。           |   default Stream<E>    |
|          ==remove(Object o)==          |  从该集合中删除指定元素的单个实例（如果存在）（可选操作）。  |        boolean         |
|       removeAll(Collection<?> c)       |      删除指定集合中包含的所有此集合的元素（可选操作）。      |        boolean         |
| removeIf(Predicate<?  super E> filter) |             删除满足给定谓词的此集合的所有元素。             |    default boolean     |
|       retainAll(Collection<?> c)       |      仅保留此集合中包含在指定集合中的元素（可选操作）。      |        boolean         |
|               ==size()==               |                    返回此集合中的元素数。                    |          int           |
|             spliterator()              |           创建一个Spliterator在这个集合中的元素。            | default Spliterator<E> |
|                stream()                |              返回以此集合作为源的顺序 Stream 。              |   default Stream<E>    |
|               toArray()                |             返回一个包含此集合中所有元素的数组。             |        Object[]        |
|             toArray(T[] a)             | 返回包含此集合中所有元素的数组;  返回的数组的运行时类型是指定数组的运行时类型。 |        <T> T[]         |