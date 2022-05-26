# Java-数据容器-集合-List

- List接口的所有实现类存储数据的方式都是==顺序==、==不唯一==的
- List的遍历方式
  - 普通for循环
  - 增强for循环
  - 遍历器 iterator()
- List的方法，常用方法黄字标底

|                    方法名                     |                        方法的详细描述                        |     方法返回值类型     |
| :-------------------------------------------: | :----------------------------------------------------------: | :--------------------: |
|                 ==add(E e)==                  |         将指定的元素追加到此列表的末尾（可选操作）。         |        boolean         |
|        ==add(int index,  E element)==         |       将指定的元素插入此列表中的指定位置（可选操作）。       |          void          |
|      addAll(Collection<?  extends E> c)       | 按指定集合的迭代器（可选操作）返回的顺序将指定集合中的所有元素附加到此列表的末尾。 |        boolean         |
| addAll(int index,  Collection<? extends E> c) | 将指定集合中的所有元素插入到此列表中的指定位置（可选操作）。 |        boolean         |
|                  ==clear()==                  |             从此列表中删除所有元素（可选操作）。             |          void          |
|            ==contains(Object o)==             |           如果此列表包含指定的元素，则返回 true 。           |        boolean         |
|         containsAll(Collection<?> c)          |       如果此列表包含指定 集合的所有元素，则返回true。        |        boolean         |
|             ==equals(Object o)==              |          将指定的对象与此列表进行比较以获得相等性。          |        boolean         |
|              ==get(int index)==               |                 返回此列表中指定位置的元素。                 |           E            |
|                ==hashCode()==                 |                    返回此列表的哈希码值。                    |          int           |
|             ==indexOf(Object o)==             | 返回此列表中指定元素的第一次出现的索引，如果此列表不包含元素，则返回-1。 |          int           |
|                 ==isEmpty()==                 |             如果此列表不包含元素，则返回 true 。             |        boolean         |
|                ==iterator()==                 |           以正确的顺序返回该列表中的元素的迭代器。           |      Iterator<E>       |
|           ==lastIndexOf(Object o)==           | 返回此列表中指定元素的最后一次出现的索引，如果此列表不包含元素，则返回-1。 |          int           |
|              ==listIterator()==               |           返回列表中的列表迭代器（按适当的顺序）。           |    ListIterator<E>     |
|          ==listIterator(int index)==          | 从列表中的指定位置开始，返回列表中的元素（按正确顺序）的列表迭代器。 |    ListIterator<E>     |
|             ==remove(int index)==             |           删除该列表中指定位置的元素（可选操作）。           |           E            |
|             ==remove(Object o)==              |  从列表中删除指定元素的第一个出现（如果存在）（可选操作）。  |        boolean         |
|          removeAll(Collection<?> c)           |    从此列表中删除包含在指定集合中的所有元素（可选操作）。    |        boolean         |
|     replaceAll(UnaryOperator<E> operator)     |    将该列表的每个元素替换为将该运算符应用于该元素的结果。    |      default void      |
|          retainAll(Collection<?> c)           |      仅保留此列表中包含在指定集合中的元素（可选操作）。      |        boolean         |
|        ==set(int index,  E element)==         |     用指定的元素（可选操作）替换此列表中指定位置的元素。     |           E            |
|                  ==size()==                   |                    返回此列表中的元素数。                    |          int           |
|        sort(Comparator<?  super E> c)         |         使用随附的 Comparator排序此列表来比较元素。          |      default void      |
|                 spliterator()                 |           在此列表中的元素上创建一个Spliterator 。           | default Spliterator<E> |
|     subList(int fromIndex,  int toIndex)      |  返回此列表中指定的 fromIndex （含）和 toIndex之间的视图。   |        List<E>         |
|                   toArray()                   | 以正确的顺序（从第一个到最后一个元素）返回一个包含此列表中所有元素的数组。 |        Object[]        |
|                toArray(T[] a)                 | 以正确的顺序返回一个包含此列表中所有元素的数组（从第一个到最后一个元素）;  返回的数组的运行时类型是指定数组的运行时类型。 |        <T> T[]         |

