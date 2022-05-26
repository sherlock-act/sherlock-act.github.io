# Java-Collections工具类

- `Collections`工具类的构造器是被私有化的，无法创建对象，并且里面所有的属性和方法都使用`static`修饰，都可以直接使用类名.方法名(属性名)直接调用。
- Collections常用方法练习

```java
package com.shanlei.test01;

import java.util.ArrayList;
import java.util.Collections;

/**
 * @author: shanlei
 * @version: 1.0
 */
public class Test01 {
    // 这是main方法，实现程序主要逻辑
    public static void main(String[] args) {
        ArrayList<String> list = new ArrayList<>();
        list.add("bb");
        Collections.addAll(list, new String[]{"cc","aa","ff"});
        Collections.addAll(list,"dd","gg","ee");
        System.out.println(list);
        // sort,排序，默认是升序
        Collections.sort(list);
        System.out.println(list);
        // binarySearch 必须是有序的集合才能查找
        System.out.println(Collections.binarySearch(list, "bb"));

        ArrayList<String> list2 = new ArrayList<>();
        Collections.addAll(list2, "tt","rr");
        //copy ,使用list2的数据对list进行替换
        // 输出结果：
       /* [tt, rr, cc, dd, ee, ff, gg]
        [tt, rr]*/
        Collections.copy(list, list2);
        System.out.println(list);
        System.out.println(list2);

        // fill 填充
        Collections.fill(list2,"yy");
        System.out.println(list2);
    }
}

```

- Collections的其他方法

| 方法名                                                       | 方法解释                                                     | 方法返回值类型                                     |
| ------------------------------------------------------------ | ------------------------------------------------------------ | -------------------------------------------------- |
| addAll(Collection<?  super T> c, T... elements)              | 将所有指定的元素添加到指定的集合。                           | static <T> boolean                                 |
| asLifoQueue(Deque<T> deque)                                  | 返回Deque作为先进先出（ Lifo ） Queue的视图 。               | static <T> Queue<T>                                |
| binarySearch(List<?  extends Comparable<? super T>> list, T key) | 使用二叉搜索算法搜索指定对象的指定列表。                     | static <T> int                                     |
| binarySearch(List<?  extends T> list, T key, Comparator<? super T> c) | 使用二叉搜索算法搜索指定对象的指定列表。                     | static <T> int                                     |
| checkedCollection(Collection<E> c,  类<E> type)              | 返回指定集合的动态类型安全视图。                             | static <E> Collection<E>                           |
| checkedList(List<E> list,  类<E> type)                       | 返回指定列表的动态类型安全视图。                             | static <E> List<E>                                 |
| checkedMap(Map<K,V> m,  类<K> keyType, 类<V> valueType)      | 返回指定地图的动态类型安全视图。                             | static <K,V> Map<K,V>                              |
| checkedNavigableMap(NavigableMap<K,V> m,  类<K> keyType, 类<V> valueType) | 返回指定可导航地图的动态类型安全视图。                       | static <K,V> NavigableMap<K,V>                     |
| checkedNavigableSet(NavigableSet<E> s,  类<E> type)          | 返回指定的可导航集的动态类型安全视图。                       | static <E> NavigableSet<E>                         |
| checkedQueue(Queue<E> queue,  类<E> type)                    | 返回指定队列的动态类型安全视图。                             | static <E> Queue<E>                                |
| checkedSet(Set<E> s,  类<E> type)                            | 返回指定集合的动态类型安全视图。                             | static <E> Set<E>                                  |
| checkedSortedMap(SortedMap<K,V> m,  类<K> keyType, 类<V> valueType) | 返回指定排序映射的动态类型安全视图。                         | static <K,V> SortedMap<K,V>                        |
| checkedSortedSet(SortedSet<E> s,  类<E> type)                | 返回指定排序集的动态类型安全视图。                           | static <E> SortedSet<E>                            |
| copy(List<?  super T> dest, List<? extends T> src)           | 将所有元素从一个列表复制到另一个列表中。                     | static <T> void                                    |
| disjoint(Collection<?> c1,  Collection<?> c2)                | 如果两个指定的集合没有共同的元素，则返回 true 。             | static boolean                                     |
| emptyEnumeration()                                           | 返回没有元素的枚举。                                         | static <T> Enumeration<T>                          |
| emptyIterator()                                              | 返回没有元素的迭代器。                                       | static <T> Iterator<T>                             |
| emptyList()                                                  | 返回空列表（immutable）。                                    | static <T> List<T>                                 |
| emptyListIterator()                                          | 返回没有元素的列表迭代器。                                   | static <T> ListIterator<T>                         |
| emptyMap()                                                   | 返回空的地图（不可变）。                                     | static <K,V> Map<K,V>                              |
| emptyNavigableMap()                                          | 返回空导航地图（不可变）。                                   | static <K,V> NavigableMap<K,V>                     |
| emptyNavigableSet()                                          | 返回一个空导航集（immutable）。                              | static <E> NavigableSet<E>                         |
| emptySet()                                                   | 返回一个空集（immutable）。                                  | static <T> Set<T>                                  |
| emptySortedMap()                                             | 返回空的排序映射（immutable）。                              | static <K,V> SortedMap<K,V>                        |
| emptySortedSet()                                             | 返回一个空的排序集（immutable）。                            | static <E> SortedSet<E>                            |
| enumeration(Collection<T> c)                                 | 返回指定集合的枚举。                                         | static <T> Enumeration<T>                          |
| fill(List<?  super T> list, T obj)                           | 用指定的元素代替指定列表的所有元素。                         | static <T> void                                    |
| frequency(Collection<?> c,  Object o)                        | 返回指定集合中与指定对象相等的元素数。                       | static int                                         |
| indexOfSubList(List<?> source,  List<?> target)              | 返回指定源列表中指定目标列表的第一次出现的起始位置，如果没有此类事件，则返回-1。 | static int                                         |
| lastIndexOfSubList(List<?> source,  List<?> target)          | 返回指定源列表中指定目标列表的最后一次出现的起始位置，如果没有此类事件则返回-1。 | static int                                         |
| list(Enumeration<T> e)                                       | 返回一个数组列表，其中包含由枚举返回的顺序由指定的枚举返回的元素。 | static <T> ArrayList<T>                            |
| max(Collection<?  extends T> coll)                           | 根据其元素的 自然顺序返回给定集合的最大元素。                | static <T extends Object &  Comparable<? super T>> |
| max(Collection<?  extends T> coll, Comparator<? super T> comp) | 根据指定的比较器引发的顺序返回给定集合的最大元素。           | static <T> T                                       |
| min(Collection<?  extends T> coll)                           | 根据其元素的 自然顺序返回给定集合的最小元素。                | static <T extends Object &  Comparable<? super T>> |
| min(Collection<?  extends T> coll, Comparator<? super T> comp) | 根据指定的比较器引发的顺序返回给定集合的最小元素。           | static <T> T                                       |
| nCopies(int n, T o)                                          | 返回由指定对象的 n副本组成的不可变列表。                     | static <T> List<T>                                 |
| newSetFromMap(Map<E,Boolean> map)                            | 返回由指定地图支持的集合。                                   | static <E> Set<E>                                  |
| replaceAll(List<T> list,  T oldVal, T newVal)                | 将列表中一个指定值的所有出现替换为另一个。                   | static <T> boolean                                 |
| reverse(List<?> list)                                        | 反转指定列表中元素的顺序。                                   | static void                                        |
| reverseOrder()                                               | 返回一个比较器，它对实现 Comparable接口的对象集合施加了 自然排序的相反。 | static <T> Comparator<T>                           |
| reverseOrder(Comparator<T> cmp)                              | 返回一个比较器，它强制指定比较器的反向排序。                 | static <T> Comparator<T>                           |
| rotate(List<?> list,  int distance)                          | 将指定列表中的元素旋转指定的距离。                           | static void                                        |
| shuffle(List<?> list)                                        | 使用默认的随机源随机排列指定的列表。                         | static void                                        |
| shuffle(List<?> list,  Random rnd)                           | 使用指定的随机源随机排列指定的列表。                         | static void                                        |
| singleton(T o)                                               | 返回一个只包含指定对象的不可变集。                           | static <T> Set<T>                                  |
| singletonList(T o)                                           | 返回一个只包含指定对象的不可变列表。                         | static <T> List<T>                                 |
| singletonMap(K key, V value)                                 | 返回一个不可变的地图，只将指定的键映射到指定的值。           | static <K,V> Map<K,V>                              |
| sort(List<T> list)                                           | 根据其元素的natural ordering对指定的列表进行排序。           | static <T extends Comparable<? super T>>           |
| sort(List<T> list,  Comparator<? super T> c)                 | 根据指定的比较器引起的顺序对指定的列表进行排序。             | static <T> void                                    |
| swap(List<?> list,  int i, int j)                            | 交换指定列表中指定位置的元素。                               | static void                                        |
| synchronizedCollection(Collection<T> c)                      | 返回由指定集合支持的同步（线程安全）集合。                   | static <T> Collection<T>                           |
| synchronizedList(List<T> list)                               | 返回由指定列表支持的同步（线程安全）列表。                   | static <T> List<T>                                 |
| synchronizedMap(Map<K,V> m)                                  | 返回由指定地图支持的同步（线程安全）映射。                   | static <K,V> Map<K,V>                              |
| synchronizedNavigableMap(NavigableMap<K,V> m)                | 返回由指定的可导航地图支持的同步（线程安全）可导航地图。     | static <K,V> NavigableMap<K,V>                     |
| synchronizedNavigableSet(NavigableSet<T> s)                  | 返回由指定的可导航集支持的同步（线程安全）可导航集。         | static <T> NavigableSet<T>                         |
| synchronizedSet(Set<T> s)                                    | 返回由指定集合支持的同步（线程安全）集。                     | static <T> Set<T>                                  |
| synchronizedSortedMap(SortedMap<K,V> m)                      | 返回由指定的排序映射支持的同步（线程安全）排序映射。         | static <K,V> SortedMap<K,V>                        |
| synchronizedSortedSet(SortedSet<T> s)                        | 返回由指定的排序集支持的同步（线程安全）排序集。             | static <T> SortedSet<T>                            |
| unmodifiableCollection(Collection<?  extends T> c)           | 返回指定集合的不可修改视图。                                 | static <T> Collection<T>                           |
| unmodifiableList(List<?  extends T> list)                    | 返回指定列表的不可修改视图。                                 | static <T> List<T>                                 |
| unmodifiableMap(Map<?  extends K,? extends V> m)             | 返回指定地图的不可修改视图。                                 | static <K,V> Map<K,V>                              |
| unmodifiableNavigableMap(NavigableMap<K,?  extends V> m)     | 返回指定可导航地图的不可修改视图。                           | static <K,V> NavigableMap<K,V>                     |
| unmodifiableNavigableSet(NavigableSet<T> s)                  | 返回指定的可导航集合的不可修改的视图。                       | static <T> NavigableSet<T>                         |
| unmodifiableSet(Set<?  extends T> s)                         | 返回指定集合的不可修改视图。                                 | static <T> Set<T>                                  |
| unmodifiableSortedMap(SortedMap<K,?  extends V> m)           | 返回指定排序映射的不可修改视图。                             | static <K,V> SortedMap<K,V>                        |
| unmodifiableSortedSet(SortedSet<T> s)                        | 返回指定排序集的不可修改视图。                               | static <T> SortedSet<T>                            |