# Java-数据容器-集合-HashSet

- HashSet是Set接口的实现类
- HashSet底层存储的原理基于哈希表实现
- HashSet底层存储是按照数组+加链表的方式进行的
- HashSet的特点
  - 无序
  - 唯一
- HashSet的方法，常用方法黄底标注

|         方法名         |                        方法详细描述                         | 方法返回值类型 |
| :--------------------: | :---------------------------------------------------------: | :------------: |
|      ==add(E e)==      |         将指定的元素添加到此集合（如果尚未存在）。          |    boolean     |
|      ==clear()==       |                  从此集合中删除所有元素。                   |      void      |
|        clone()         |      返回此 HashSet实例的浅层副本：元素本身不被克隆。       |     Object     |
| ==contains(Object o)== |          如果此集合包含指定的元素，则返回 true 。           |    boolean     |
|     ==isEmpty()==      |            如果此集合不包含元素，则返回 true 。             |    boolean     |
|     ==iterator()==     |                 返回此集合中元素的迭代器。                  |  Iterator<E>   |
|  ==remove(Object o)==  |           如果存在，则从该集合中删除指定的元素。            |    boolean     |
|       ==size()==       |              返回此集合中的元素数（其基数）。               |      int       |
|     spliterator()      | 在此集合中的元素上创建late-binding和故障快速 Spliterator 。 | Spliterator<E> |