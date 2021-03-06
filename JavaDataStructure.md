* java.util包中三个重要的接口及特点：List（列表）、Set（保证集合中元素唯一）、Map（维护多个key-value键值对，保证key唯一）。
Collection  
├List  
│├LinkedList  
│├ArrayList  
│└Vector  
│　└Stack   
└Set  
Map  
├Hashtable  
├HashMap  
└WeakHashMap  

#Collection接口
* Collection是最基本的集合接口，一个Collection代表一组Object，即Collection的元素（Elements）。一些Collection允许相同的元素而另一些不行。一些能排序而另一些不行。Java SDK不提供直接继承自Collection的类，Java SDK提供的类都是继承自Collection的“子接口”如List和Set。所有实现Collection接口的类都必须提供两个标准的构造函数：无参数的构造函数用于创建一个空的Collection，有一个Collection参数的构造函数用于创建一个新的Collection，这个新的Collection与传入的Collection有相同的元素。后一个构造函数允许用户复制一个Collection。

* 由Collection接口派生的两个接口是List和Set。
* 主要方法:  
boolean add(Object o)添加对象到集合  
boolean remove(Object o)删除指定的对象 
int size()返回当前集合中元素的数量  
boolean contains(Object o)查找集合中是否有指定的对象 
boolean isEmpty()判断集合是否为空  
Iterator iterator()返回一个迭代器  
boolean containsAll(Collection c)查找集合中是否有集合c中的元素  
boolean addAll(Collection c)将集合c中所有的元素添加给该集合  
void clear()删除集合中所有元素  
void removeAll(Collection c)从集合中删除c集合中也有的元素  
void retainAll(Collection c)从集合中删除集合c中不包含的元素

##List接口
*  List是有序的Collection，使用此接口能够精确的控制每个元素插入的位置。用户能够使用索引（元素在List中的位置，类似于数组下标）来访问List中的元素，这类似于Java的数组。除了具有Collection接口必备的iterator()方法外，List还提供一个listIterator()方法，返回一个ListIterator接口，和标准的Iterator接口相比，ListIterator多了一些add()之类的方法，允许添加，删除，设定元素，还能向前或向后遍历。

*  ArrayList、Vector是线性表，使用Object数组作为容器去存储数据的，添加了很多方法维护这个数组，使其容量可以动态增长，极大地提升了开发效率。它们明显的区别是ArrayList是非同步的，Vector是同步的。不用考虑多线程时应使用ArrayList来提升效率。LinkedList是链表，略懂数据结构就知道其实现原理了。链表随机位置插入、删除数据时比线性表快，遍历比线性表慢。
*  由此可根据实际情况来选择使用ArrayList（非同步、非频繁删除时选择）、Vector（需同步时选择）、LinkedList（频繁在任意位置插入、删除时选择）。
    
##Map接口
* Map没有继承Collection接口，Map提供key到value的映射。一个Map中不能包含相同的key，每个key只能映射一个value。Map接口提供3种集合的视图，Map的内容可以被当作一组key集合，一组value集合，或者一组key-value映射。

* Hashtable继承Map接口，实现一个key-value映射的哈希表。任何非空（non-null）的对象都可作为key或者value。Hashtable是同步的。
* HashMap和Hashtable类似，不同之处在于HashMap是非同步的，并且允许null，即null value和null key。，但是将HashMap视为Collection时（values()方法可返回Collection），其迭代子操作时间开销和HashMap的容量成比例。因此，如果迭代操作的性能相当重要的话，不要将HashMap的初始化容量设得过高，或者load factor过低。

* WeakHashMap是一种改进的HashMap，它对key实行“弱引用”，如果一个key不再被外部所引用，那么该key可以被GC回收。
    
##Set接口
* Set是一种不包含重复的元素的Collection，Set结构其实就是维护一个Map来存储数据的，利用Map结构key值唯一性。HashSet、TreeSet分别默认维护一个HashMap、TreeMap。
    
#总结
* 如果涉及到堆栈，队列等操作，应该考虑用List，对于需要快速插入，删除元素，应该使用LinkedList，如果需要快速随机访问元素，应该使用ArrayList。

* 如果程序在单线程环境中，或者访问仅仅在一个线程中进行，考虑非同步的类，其效率较高，如果多个线程可能同时操作一个类，应该使用同步的类。
* 要特别注意对哈希表的操作，作为key的对象要正确复写equals和hashCode方法。

* 尽量返回接口而非实际的类型，如返回List而非ArrayList，这样如果以后需要将ArrayList换成LinkedList时，客户端代码不用改变。这就是针对抽象编程。
   
