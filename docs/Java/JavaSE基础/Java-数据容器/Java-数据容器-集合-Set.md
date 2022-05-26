# Java-数据容器-集合-Set

- Set是继承自Collection接口的接口
- Set没有索引相关的方法，也就是说没有办法使用普通for循环进行遍历
- Set的遍历方式
  - 增强for循环
  - 迭代器
- Set存储是==无序==且==唯一==的
  - 无序主要的底层原理是基于HashMap的原理实现的
  - 唯一的特点主要是基于hashcode方法与equals方法对元素进行比较实现的
  - 如果Set用来存放自定义对象的时候，要想实现唯一的特点，那么存放对象的类必须重写hashcode与equals方法
- Set的方法，常用的方法黄底标注

|               方法名               |                         方法详细说明                         |     方法返回值类型     |
| :--------------------------------: | :----------------------------------------------------------: | :--------------------: |
|            ==add(E e)==            |   如果指定的元素不存在，则将其指定的元素添加（可选操作）。   |        boolean         |
| addAll(Collection<?  extends E> c) | 将指定集合中的所有元素添加到此集合（如果尚未存在）（可选操作）。 |        boolean         |
|            ==clear()==             |             从此集合中删除所有元素（可选操作）。             |          void          |
|       ==contains(Object o)==       |           如果此集合包含指定的元素，则返回 true 。           |        boolean         |
|    containsAll(Collection<?> c)    |         返回 true如果此集合包含所有指定集合的元素。          |        boolean         |
|        ==equals(Object o)==        |           将指定的对象与此集合进行比较以实现相等。           |        boolean         |
|           ==hashCode()==           |                    返回此集合的哈希码值。                    |          int           |
|           ==isEmpty()==            |             如果此集合不包含元素，则返回 true 。             |        boolean         |
|           ==iterator()==           |                  返回此集合中元素的迭代器。                  |      Iterator<E>       |
|        ==remove(Object o)==        |      如果存在，则从该集合中删除指定的元素（可选操作）。      |        boolean         |
|     removeAll(Collection<?> c)     |     从此集合中删除指定集合中包含的所有元素（可选操作）。     |        boolean         |
|     retainAll(Collection<?> c)     |      仅保留该集合中包含在指定集合中的元素（可选操作）。      |        boolean         |
|             ==size()==             |               返回此集合中的元素数（其基数）。               |          int           |
|           spliterator()            |          在此集合中的元素上创建一个 Spliterator 。           | default Spliterator<E> |
|             toArray()              |             返回一个包含此集合中所有元素的数组。             |        Object[]        |
|           toArray(T[] a)           | 返回一个包含此集合中所有元素的数组;  返回的数组的运行时类型是指定数组的运行时类型。 |        <T> T[]         |