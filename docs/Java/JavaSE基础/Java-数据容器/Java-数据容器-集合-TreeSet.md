# Java-数据容器-集合-TreeSet

- TreeSet是Set接口的实现类
- TreeSet底层存储必须实现内部或者外部比较器
- TreeSet底层存储的原理是通过比较器进行比较后按照二叉树的原理进行存放
- TreeSet的特点
  - 相对有序（TreeSet的数据按照升序进行遍历）
  - 唯一
- TreeSet的方法

|                            方法名                            |                         方法详细描述                         |    方法返回值类型     |
| :----------------------------------------------------------: | :----------------------------------------------------------: | :-------------------: |
|                           add(E e)                           |          将指定的元素添加到此集合（如果尚未存在）。          |        boolean        |
|              addAll(Collection<?  extends E> c)              |            将指定集合中的所有元素添加到此集合中。            |        boolean        |
|                         ceiling(E e)                         | 返回此集合中最小元素大于或等于给定元素，如果没有此元素，则返回 null 。 |           E           |
|                           clear()                            |                   从此集合中删除所有元素。                   |         void          |
|                           clone()                            |                 返回此 TreeSet实例的浅拷贝。                 |        Object         |
|                         comparator()                         | 返回用于对该集合中的元素进行排序的比较器，或null，如果此集合使用其元素的natural ordering 。 | Comparator<? super E> |
|                      contains(Object o)                      |           如果此集合包含指定的元素，则返回 true 。           |        boolean        |
|                     descendingIterator()                     |              以降序返回该集合中的元素的迭代器。              |      Iterator<E>      |
|                       descendingSet()                        |            返回此集合中包含的元素的反向排序视图。            |    NavigableSet<E>    |
|                           first()                            |            返回此集合中当前的第一个（最低）元素。            |           E           |
|                          floor(E e)                          | 返回此集合中最大的元素小于或等于给定元素，如果没有这样的元素，则返回  null 。 |           E           |
|                     headSet(E toElement)                     |     返回此集合的部分的视图，其元素严格小于 toElement 。      |     SortedSet<E>      |
|           headSet(E toElement,  boolean inclusive)           | 返回该集合的部分的视图，其元素小于（或等于，如果 inclusive为真） toElement 。 |    NavigableSet<E>    |
|                         higher(E e)                          | 返回严格大于给定元素的该集合中的最小元素，如果没有此元素则返回 null 。 |           E           |
|                          isEmpty()                           |             如果此集合不包含元素，则返回 true 。             |        boolean        |
|                          iterator()                          |              以升序返回该集合中的元素的迭代器。              |      Iterator<E>      |
|                            last()                            |             返回此集合中当前的最后（最高）元素。             |           E           |
|                          lower(E e)                          | 返回这个集合中最大的元素严格小于给定的元素，如果没有这样的元素，则返回  null 。 |           E           |
|                         pollFirst()                          |  检索并删除第一个（最低）元素，或返回 null如果该集合为空。   |           E           |
|                          pollLast()                          | 检索并删除最后一个（最高）元素，如果此集合为空，则返回 null 。 |           E           |
|                       remove(Object o)                       |            如果存在，则从该集合中删除指定的元素。            |        boolean        |
|                            size()                            |               返回此集合中的元素数（其基数）。               |          int          |
|                        spliterator()                         | 在此集合中的元素上创建late-binding和故障切换 Spliterator 。  |    Spliterator<E>     |
| subSet(E fromElement,  boolean fromInclusive, E toElement, boolean toInclusive) | 返回该集合的部分的视图，其元素的范围从 fromElement到 toElement 。 |    NavigableSet<E>    |
|             subSet(E fromElement,  E toElement)              | 返回此集合的部分的视图，其元素的范围从 fromElement （含）到 toElement ，排他。 |     SortedSet<E>      |
|                    tailSet(E fromElement)                    |     返回此组件的元素大于或等于 fromElement的部分的视图。     |     SortedSet<E>      |
|          tailSet(E fromElement,  boolean inclusive)          | 返回此集合的部分的视图，其元素大于（或等于，如果 inclusive为真） fromElement 。 |    NavigableSet<E>    |