# Java-数据容器-集合-LinkedList

- LinkedList是List接口的实现类 
- LinkedList底层数据存储方式是跳转结构进行存储的，是双向链表
- LinkedList的优点
  - 删除、增加元素效率高
  - 数据可重复
- LinkedList的缺点
  - 遍历效率低
- LinkedList的方法，常用方法黄底标注

|                    方法名                     |                         方法详细描述                         | 方法返回值类型  |
| :-------------------------------------------: | :----------------------------------------------------------: | :-------------: |
|                 ==add(E e)==                  |               将指定的元素追加到此列表的末尾。               |     boolean     |
|        ==add(int index,  E element)==         |             在此列表中的指定位置插入指定的元素。             |      void       |
|      addAll(Collection<?  extends E> c)       | 按照指定集合的迭代器返回的顺序将指定集合中的所有元素追加到此列表的末尾。 |     boolean     |
| addAll(int index,  Collection<? extends E> c) |   将指定集合中的所有元素插入到此列表中，从指定的位置开始。   |     boolean     |
|               ==addFirst(E e)==               |                 在该列表开头插入指定的元素。                 |      void       |
|               ==addLast(E e)==                |               将指定的元素追加到此列表的末尾。               |      void       |
|                  ==clear()==                  |                    从列表中删除所有元素。                    |      void       |
|                    clone()                    |                 返回此 LinkedList的浅版本。                  |     Object      |
|            ==contains(Object o)==             |           如果此列表包含指定的元素，则返回 true 。           |     boolean     |
|           ==descendingIterator()==            |          以相反的顺序返回此deque中的元素的迭代器。           |   Iterator<E>   |
|                 ==element()==                 |            检索但不删除此列表的头（第一个元素）。            |        E        |
|              ==get(int index)==               |                 返回此列表中指定位置的元素。                 |        E        |
|                ==getFirst()==                 |                  返回此列表中的第一个元素。                  |        E        |
|                 ==getLast()==                 |                 返回此列表中的最后一个元素。                 |        E        |
|             ==indexOf(Object o)==             | 返回此列表中指定元素的第一次出现的索引，如果此列表不包含元素，则返回-1。 |       int       |
|           ==lastIndexOf(Object o)==           | 返回此列表中指定元素的最后一次出现的索引，如果此列表不包含元素，则返回-1。 |       int       |
|          ==listIterator(int index)==          | 从列表中的指定位置开始，返回此列表中元素的列表迭代器（按适当的顺序）。 | ListIterator<E> |
|                ==offer(E e)==                 |       将指定的元素添加为此列表的尾部（最后一个元素）。       |     boolean     |
|              ==offerFirst(E e)==              |                在此列表的前面插入指定的元素。                |     boolean     |
|              ==offerLast(E e)==               |                在该列表的末尾插入指定的元素。                |     boolean     |
|                  ==peek()==                   |            检索但不删除此列表的头（第一个元素）。            |        E        |
|                ==peekFirst()==                | 检索但不删除此列表的第一个元素，如果此列表为空，则返回 null 。 |        E        |
|                ==peekLast()==                 | 检索但不删除此列表的最后一个元素，如果此列表为空，则返回 null 。 |        E        |
|                  ==poll()==                   |             检索并删除此列表的头（第一个元素）。             |        E        |
|                ==pollFirst()==                | 检索并删除此列表的第一个元素，如果此列表为空，则返回 null 。 |        E        |
|                ==pollLast()==                 | 检索并删除此列表的最后一个元素，如果此列表为空，则返回 null 。 |        E        |
|                   ==pop()==                   |              从此列表表示的堆栈中弹出一个元素。              |        E        |
|                 ==push(E e)==                 |              将元素推送到由此列表表示的堆栈上。              |      void       |
|                 ==remove()==                  |             检索并删除此列表的头（第一个元素）。             |        E        |
|             ==remove(int index)==             |                 删除该列表中指定位置的元素。                 |        E        |
|             ==remove(Object o)==              |        从列表中删除指定元素的第一个出现（如果存在）。        |     boolean     |
|               ==removeFirst()==               |               从此列表中删除并返回第一个元素。               |        E        |
|        removeFirstOccurrence(Object o)        |   删除此列表中指定元素的第一个出现（从头到尾遍历列表时）。   |     boolean     |
|               ==removeLast()==                |              从此列表中删除并返回最后一个元素。              |        E        |
|        removeLastOccurrence(Object o)         |  删除此列表中指定元素的最后一次出现（从头到尾遍历列表时）。  |     boolean     |
|        ==set(int index,  E element)==         |           用指定的元素替换此列表中指定位置的元素。           |        E        |
|                  ==size()==                   |                    返回此列表中的元素数。                    |       int       |
|                 spliterator()                 | 在此列表中的元素上创建late-binding和故障快速 Spliterator 。  | Spliterator<E>  |
|                   toArray()                   | 以正确的顺序（从第一个到最后一个元素）返回一个包含此列表中所有元素的数组。 |    Object[]     |
|                toArray(T[] a)                 | 以正确的顺序返回一个包含此列表中所有元素的数组（从第一个到最后一个元素）;  返回的数组的运行时类型是指定数组的运行时类型。 |     <T> T[]     |