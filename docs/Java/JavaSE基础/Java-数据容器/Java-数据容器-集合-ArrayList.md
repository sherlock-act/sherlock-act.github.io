# Java-数据容器-集合-ArrayList

- ArrayList是List接口的实现类 
- ArryaList底层数据存储方式是数组的形式，链式结构进行存储
- ArrayList的优点
  - 查询效率高
  - 数据可重复
- ArrayList的缺点
  - 删除、增加元素效率低
- ArrayList的方法，常用方法黄底标注

|                    方法名                     |                         方法详细描述                         | 方法返回值类型  |
| :-------------------------------------------: | :----------------------------------------------------------: | :-------------: |
|                 ==add(E e)==                  |               将指定的元素追加到此列表的末尾。               |     boolean     |
|        ==add(int index,  E element)==         |             在此列表中的指定位置插入指定的元素。             |      void       |
|      addAll(Collection<?  extends E> c)       | 按指定集合的Iterator返回的顺序将指定集合中的所有元素追加到此列表的末尾。 |     boolean     |
| addAll(int index,  Collection<? extends E> c) |   将指定集合中的所有元素插入到此列表中，从指定的位置开始。   |     boolean     |
|                  ==clear()==                  |                    从列表中删除所有元素。                    |      void       |
|                    clone()                    |                返回此 ArrayList实例的浅拷贝。                |     Object      |
|            ==contains(Object o)==             |           如果此列表包含指定的元素，则返回 true 。           |     boolean     |
|        ensureCapacity(int minCapacity)        | 如果需要，增加此 ArrayList实例的容量，以确保它可以至少保存最小容量参数指定的元素数。 |      void       |
|     forEach(Consumer<?  super E> action)      | 对 Iterable的每个元素执行给定的操作，直到所有元素都被处理或动作引发异常。 |      void       |
|              ==get(int index)==               |                 返回此列表中指定位置的元素。                 |        E        |
|             ==indexOf(Object o)==             | 返回此列表中指定元素的第一次出现的索引，如果此列表不包含元素，则返回-1。 |       int       |
|                 ==isEmpty()==                 |             如果此列表不包含元素，则返回 true 。             |     boolean     |
|                ==iterator()==                 |           以正确的顺序返回该列表中的元素的迭代器。           |   Iterator<E>   |
|           ==lastIndexOf(Object o)==           | 返回此列表中指定元素的最后一次出现的索引，如果此列表不包含元素，则返回-1。 |       int       |
|              ==listIterator()==               |           返回列表中的列表迭代器（按适当的顺序）。           | ListIterator<E> |
|          ==listIterator(int index)==          | 从列表中的指定位置开始，返回列表中的元素（按正确顺序）的列表迭代器。 | ListIterator<E> |
|             ==remove(int index)==             |                 删除该列表中指定位置的元素。                 |        E        |
|             ==remove(Object o)==              |        从列表中删除指定元素的第一个出现（如果存在）。        |     boolean     |
|          removeAll(Collection<?> c)           |           从此列表中删除指定集合中包含的所有元素。           |     boolean     |
|    removeIf(Predicate<?  super E> filter)     |             删除满足给定谓词的此集合的所有元素。             |     boolean     |
|   removeRange(int fromIndex,  int toIndex)    | 从这个列表中删除所有索引在 fromIndex （含）和 toIndex之间的元素。 | protected void  |
|     replaceAll(UnaryOperator<E> operator)     |    将该列表的每个元素替换为将该运算符应用于该元素的结果。    |      void       |
|          retainAll(Collection<?> c)           |            仅保留此列表中包含在指定集合中的元素。            |     boolean     |
|        ==set(int index,  E element)==         |           用指定的元素替换此列表中指定位置的元素。           |        E        |
|                  ==size()==                   |                    返回此列表中的元素数。                    |       int       |
|      ==sort(Comparator<?  super E> c)==       |      使用提供的 Comparator对此列表进行排序以比较元素。       |      void       |
|                 spliterator()                 | 在此列表中的元素上创建late-binding和故障快速 Spliterator 。  | Spliterator<E>  |
|     subList(int fromIndex,  int toIndex)      | 返回此列表中指定的 fromIndex （包括）和 toIndex之间的独占视图。 |     List<E>     |
|                   toArray()                   | 以正确的顺序（从第一个到最后一个元素）返回一个包含此列表中所有元素的数组。 |    Object[]     |
|                toArray(T[] a)                 | 以正确的顺序返回一个包含此列表中所有元素的数组（从第一个到最后一个元素）;  返回的数组的运行时类型是指定数组的运行时类型。 |     <T> T[]     |
|                 trimToSize()                  |        修改这个 ArrayList实例的容量是列表的当前大小。        |      void       |

