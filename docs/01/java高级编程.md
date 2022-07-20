# java高级编程

## 1、常用API类型

## 2、集合

### 2.1集合概念

集合是一种对象容器，用于存放对象，和数组的职能类似，可理解为一种另类的数组，但是由于数组明显的缺点，所以开发出集合这一类工具。

数组的缺点：

1、根据内容查找元素速度慢 

2、数组的大小一经确定不能改变 

3、数组只能存储一种类型的数据 

### 2.2collection接口

collection接口时每个单列集合的顶层接口，也就是每个集合接口都继承或者间接继承collection接口，每个集合实现类都实现或者间接实现collection接口。

collection接口的常用方法有：

add：向集合中添加元素（返回布尔类型）

~~~java
Collection coll = new ArrayList();//Collection是接口不能new对象，这里选择实现类ArrayList实现
coll.add("rivtto");
coll.add("rivtto",1);//后者是索引位置
~~~



clear：清空集合内元素（返回布尔类型）

~~~java
coll.clear();
~~~



remove：移除集合中某元素（返回布尔类型）

~~~java
coll.remove(0);//0是索引位置
~~~



isEmpty：判断集合是否为空（返回布尔类型）

~~~java
coll.isEmpty();
~~~



contains：判断集合是否含有该元素（返回布尔类型）

~~~java
coll.contains("rivtto");
~~~



toArray：将集合转化为数组（返回Object（泛型）类型）

~~~java
coll.toArray();
~~~



addAll：向集合中添加另一个集合（返回布尔类型）

~~~java
 coll.addAll(col);
~~~



size：求出集合长度（返回int类型）

~~~java
coll.size()
~~~



removeAll：在集合中移除另一个集合（返回布尔类型）

```
coll.removeAll(col);
```

containsAll：判断集合是否含有该集合（返回布尔类型）

~~~java
coll.containsAll(col);
~~~



### 2.3迭代器

原理：迭代是重复反馈过程的活动,其⽬的通常是为了逼近所需⽬标或结果。每⼀次对过程的重复称为⼀次“迭代” , ⽽每⼀次迭代得到的结果会作为下⼀次迭代的初始值。 

~~~java
Iterator it = coll.iterator();//iterator方法返回一个Iterater对象
~~~

使用迭代器可使用其三个功能。

~~~java
it.hasNext();//从开头开始判断集合是否有值（只判断一个）  返回布尔类型
~~~

~~~java
it.next();//将游标当前数值获得，并且游标下移
~~~

~~~java
it.remove()//移除当前游标对应元素
~~~

可以组合使用，遍历集合：

~~~java
while(iterator.hasNext()){
            System.out.println(iterator.next());
        }
~~~



迭代器使用的常见问题：

1、迭代器迭代完成之后，迭代器的位置在最后⼀位。 所以迭代器只能迭代⼀次 

~~~java
while(iterator.hasNext()){
            System.out.println(iterator.next());
        }
while(iterator.hasNext()){
            System.out.println(iterator.next());
        }//两次迭代也只会执行一次
~~~



2、迭代器在迭代的时候，不要调⽤多次next⽅法，可能会出错 NoSuchElementException 

~~~java
 while(iterator.hasNext()){
            Object obj = iterator.next();
            System.out.println(iterator.next());
        }//因为使用一次指针下移。
~~~



3、在迭代器迭代的时候，不能向集合中添加或者删除元素 ConcurrentModificationException 

~~~java
 while(iterator.hasNext()){
            coll.add("iuiy");
            System.out.println(iterator.next());
        }//同时做两件事是做不到的
~~~

### 2.4ArrayList集合实现类

这是一个基于List接口实现的集合实现类：

具体关系为Collection——>List——>ArrayList



（拓展：List接口集合特点：1、有序（插入顺序）2、可以放重复元素）



ArrayList类功能是基于数组的数据结构实现

————————————————————————————————————————————-—————

ArrayList集合的特点

```
1、基于数组实现的额，具备了数组所有的优点
2、动态扩容 
3、随机查找速度非常快（基于下标访问的），随机插入非常慢，如果插入的index非常靠前，那么后面的每一个元素都要为前一个元素腾出位置来
```



——————————————————————————————————————————————————



ArrayList类常用方法有（除去以上父接口演示方法）

set：更改集合中指定索引位置的元素，并且将老元素返回。

~~~java
Object obj =coll.set(1,"78");//(与add不同的是add是指定位置增加，而它是替换)
~~~

get：获取集合中指定索引位置元素。

```
coll.get(1)；
```

subList：截取集合中指定下标开始到结束位置上的元素 

~~~java
List list= coll.subList(1,2);
~~~

indexOf：找到指定元素，并且返回该索引

~~~java
coll.indexOf("666")；
~~~



拓展：System.arraycopy（），System类的arraycopy方法，实现指定范围拷贝u共5个参数：

```
System.arraycopy(data, index + 1, data, index, (size - index - 1));

参数1：从哪个数组拷贝出来
参数2：从原先这个数组的第几个位置开始拷贝
参数3：拷贝到哪里去
参数4：拷贝的元素放到目标数组里面，是从第几个位置开始放置
参数5：一共需要拷贝多少元素
```

### 2.5LinkedList集合实现类

这是一个基于List接口实现的集合实现类：

具体关系为Collection——>List——>LinkedList



——————————————————————————————————————————————————

LinkedList集合的特点;

```
LinkedList 是一个基于Node（节点）来实现的虚拟容器（没有具体的边界），每一个节点都会从"前"和"后"两个方向记住临近节点的信息
双向链表
优点：
1、随机访问的速度比较慢，但是随机插入、删除的速度比较快（链表结构，相比数组而言增删快很多）
```

——————————————————————————————————————————————————

LinkedList的常用方法：

大多与ArrayList实现类相同有几个特例方法：

1、addFirst/addLast：在最前一位/最后一位添加数据

~~~java
coll.addFirst("第一");
coll.addLast("99");
~~~

2、getFirst/getLast：获取最前一位/最后一位的元素

```
coll.getFirst()；
coll.getLast()
```

3、push ：同addFirst（不做演示）

4、offer ：同add（不做演示）



### 2.6Map接口

Map集合是双列集合顶点，由key和value组成。

称之为键值对 

键的特点：⽆序，⽆下标，不重复。 

值的特点：⽆序，⽆下标 



Map接口的集合可理解为由两组数据组成，一组为key，一组为value，key的作用相当于数组的下标，value的作用相当于数组的值。

### 2.7HashMap集合实现类

这是一个基于Map接口实现的集合实现类：

具体关系为Map——>HashMap;

——————————————————————————————————————————————————

HashMap集合实现类的特点

```
 1、基于键值对(key-value)的数据结构
 2、它的key是不能重复的，value是可以重复的（后续增加同样的value会替代之前的value）
 3、元素的排列顺序是无法得到保障的
```

——————————————————————————————————————————————————

HashMap集合的常用方法：（大多方法和Collection相同）

put(K key, V value)：将数据放入集合中，相当于前面的add方法（第一个参数为key值，第二个参数为value）

~~~java
Map<String,String> map = new HashMap<>();
map.put("1","数据1");
~~~

get(Object key)：根据key值获取对应的value

~~~java
map.get("1")
~~~

Set keySet()：获取所有的value值，但是返回的是一个Set对象

~~~java
Set set = map.keySet();
~~~

map.containsKey("xjp"))：判断是否包含指定的key（不演示）

map.containsValue("中国") :判断是否包含指定的value （不演示）

 Collection values():获取集合内所有的Value，但是返回的是Collection对象

~~~java
Collection coll = map.values();
~~~

 Set entrySet() ：返回集合所有的key和value，返回值是Set对象

~~~jav
Set set = map.entrySet();
~~~

•boolean containsKey(Object key) 

•boolean containsValue(Object value) 

•V remove(Object key) 

•int size( 



