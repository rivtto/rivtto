#                                                                                                                                                                                                                                                                                    java高级编程

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
1、基于数组实现的，具备了数组所有的优点
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



拓展：System.arraycopy（），System类的arraycopy方法，实现指定范围拷贝，共5个参数：

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

map.containsKey("xjp"))：判断是否包含指定的key

~~~java
（不演示）
~~~

map.containsValue("中国") :判断是否包含指定的value 

~~~java
（不演示）
~~~

 Collection values():获取集合内所有的Value，但是返回的是Collection对象

~~~java
Collection coll = map.values();
~~~

 Set entrySet() ：返回集合所有的key和value，返回值是Set对象

~~~jav
Set set = map.entrySet();
~~~

boolean containsKey(Object key) ：查找是否包含该key值，返回布尔类型

~~~java
map.containsKey("4");
~~~

boolean containsValue(Object value) 

~~~java
(同上，不再演示)
~~~

remove(Object key) ：移除数据，返回泛型，（返回所移除的数据）

~~~java
(同上，不再演示)
~~~

int size( ）：获取集合长度，返回int

~~~jav
map.size();
~~~



### 2.8HashSet实现类 

这是一个基于Set接口的集合实现类

具体关系为Collection——>Set——>HashSet

（Set特点：不能存放同一个元素）

——————————————————————————————————————————————————

HashSet特点：1、无序性

​			  2、不可重复（相当于HashMap中key值的特点）

——————————————————————————————————————————————————

常用方法与ArrayList相同，不多赘述。



——————————————————————————————————————————————————

多用于去重实现

实例：

~~~java
static String[] duplicatedPlus (String[] arr) {       
    // 首先把数组转换成Collection    
    List<String> list = Arrays.asList(arr);  
    // HashSet 把所有的元素依次放入 
    Set<String> set = new HashSet<>(list);
	return  set.toArray(new String[0]);
~~~

### 2.9LinkedHashSet实现类 、TreeSet实现类 、HashTable 实现类

![1658394893964](D:\桌面\rivtto\docs\01\插图\1658394893964.png)





![1658394961736](D:\桌面\rivtto\docs\01\插图\1658394961736.png)



由以上两图片，可以得出各个实现类与其接口、父类关系。

我们也可以有图片，得到这三大实现类特点：



——————————————————————————————————————————————————

LinkedHashSet实现类：

由图可知，他有linked类，HashSet类的特点

1、有序      

2、数值唯一   



常用方法和父接口相同

——————————————————————————————————————————————————



TreeSet类 TreeSet特点：

1、⽆序(但是有字典顺序) 

2、⽆下标 

3、不可重复 

常⽤⽅法 与 HashSet 类的⽅法⼀致 

特点： 使⽤ TreeSet 集合存储对象的时候，对象必须要实现Comparable接⼝ 

实现原理 TreeSet 在存储元素的时候，会调⽤ compareTo ⽅法。两个作⽤： 

1、排序: 返回值⼤于0升序，返回值⼩于0降序 

2、去重(返回值为0) TreeSet 认为返回0，两个对象就是相同 

——————————————————————————————————————————————————

HashTable Hashtable常⽤⽅法与HashMap⼀致

 HashMap与Hashtable区别： 

1、Hashtable是线程安全的，HashMap是线程不安全的 

2、Hashtable中不允许存储null作为key和value，⽽HashMap可以 在实际开发中⼀般都是⽤HashMap。考虑线程安全使⽤ConCurrentHashMap 

### 额外知识点：

Collections⼯具类 

集合： ⼯具类(Collections) 

Collections.reverse(List list)：反序，将集合的顺序调换

~~~java
Collections.reverse(coll);
~~~

Collections.shuffle(List list)：打乱顺序，将集合数据的顺序打乱

~~~java
Collections.shuffle(coll);
~~~

Collections.sort(List list) ：排序，按数据首位ascii码，从大到小排列

~~~java
Collections.sort(coll);
~~~

——————————————————————————————————————————————————

泛型概括：

将某一数据类型用  <字母>  表示，意为该类型可变，当你调用用泛型修饰的类、接口、方法时，可在<>中输入某一固定的数据类型，表示该泛型限制为输入的数据类型。



## 3、异常

### 3.1异常的概念

异常是在程序执行时出现的错误，我们分为两类：

一类是error：这是开发人员无法处理的错误，也不需要我们处理，可理解为javaJDK的错误。

一类是Exception：这就是我们所说的异常，是可以被处理掉的，我们应该学习的东西。

这两类的出现都会导致JVM终止，使得程序无法继续下去。

### 3.2异常的分类

我们把所有的异常都归为两类：

一是RuntimeException：这是表示运行时错误，也理解为，不太致命的异常

另一是Exception：除去RuntimeException异常的其他都归为这一类。

这两类都是Throwable类的子类。

### 3.3异常的处理之try   catch

假如我们执行如下语句：

~~~java
System.out.println(3/0);
System.out.println(1);
~~~

我们知道除数是不可以为0的，所以这就是一个异常。当JVM逐句执行到这里时，就会出现错误警告，终止程序，这一句后面的语句无法执行。                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 

那么我们要做的就是，处理这个异常，就算它出现这个错误，我们也要让程序继续执行，并给出提示，我们就会用到try   catch语句处理

~~~java
try {
            System.out.println(3/num);
        }catch (Exception e){
            System.out.println("出错了");
        }
        System.out.println(1);
~~~

这样我们就会发现，程序就会跳过出现异常的那一部分，进而执行catch里面的语句，我们可以理解为不执行错误语句，转而执行错误的提示或者补偿语句。

try  catch语句是自己处理错误



### 3.4异常处理之throw

throw我们称之为抛出异常，利用try  catch抓住可能出现异常的语句，然后不在catch中写异常的处理，而是写抛出异常，让方法的执行者处理。

~~~java
 public static void main(String[] args) {
    math();
    }

    private static void math() {
        try {
            System.out.println(10/0);
        }catch(Exception e){
            throw new RuntimeException();
        }
    }
~~~

这里便是一个典型的抛出异常，语法上没有任何问题，但是我们稍加修改：

~~~java
 public static void main(String[] args) {
    math();
    }

    private static void math() {
        try {
            System.out.println(10/0);
        }catch(Exception e){
            throw new Exception();
        }
    }
~~~

这里却出现了语法上的报错，这是为什么呢？

可以看到两份代码唯一出现的不同，就是throw后面抛出的异常名称不同。

这里我们就回到开头介绍的异常分类Exception 和 RuntimeException的不同， RuntimeException我们语法上认为这是不严重的异常，就算把他抛出给方法调用者，不处理，也不会语法报错

而Exception是严重错误，一定需要处理！

~~~java
public static void main(String[] args) {
        try {
            math();
        }catch (Exception e){
            System.out.println("运算出错");
        }
    
    }

    private static void math() throws Exception{
        try {
            System.out.println(10/0);
        }catch(Exception e){
            throw new Exception();
        }
    }
~~~

这是处理后的代码，可以看到，在main方法调用时，处理了异常语法并没有报错。

同时，在math计算方法后面，添加了throws Exception的标识语句（throws 不是throw），这是严重异常方法，需要抛出异常的标识，让调用者知道调用方法需要处理。

### 3.5自定义异常

我们进入JDK底层代码，可以发现Exception类基本没有实现异常类独有方法属性，只有一个空壳，我们可以了解到，异常重要的只是一个名字，起提示作用，所以我们也可以写出异常类，继承异常主要父类Exception即可起到作用：

~~~java
class ChuShuException extends Exception{
    public ChuShuException(){
        super();
    }
    public ChuShuException(String msg){
        super(msg);
    }
}
~~~

这里可以看到，我们自定义了一个除数异常类，那么我们应该怎么使用它呢？

~~~java
public static void main(String[] args) {
        try {
           math(0);
        }catch (Exception e){
           e.printStackTrace();
        }

    }

    private static void math(int chuShu) throws ChuShuException{
       int a = 20;
       if (chuShu == 0){
           throw new ChuShuException("除数为0");
       }else{
           System.out.println(a/chuShu);
       }
    }
~~~

当我们运行时，打印出来的错误便是ChuShuException和提示”除数为0”。

e.printStackTrace()的意思是，打印出栈内触发的警告，也就是我们触发的异常。



## 4、IO流

### 4.1IO流的介绍

IO流的概念：在程序中数据，我们要读取，转移数据到另一个地方，我们使用的是一种被称之为“流”的传输技术，可理解为，复制粘贴之类操作的细节过程。

就是把文件细化成一段段数据，进行传输

![1658492582865](D:\桌面\rivtto\docs\01\插图\1658492582865.png)



可以看到IO流的知识点非常多，但是以后的开发中，我们会使用各种帮助类实现IO流的操作，所以我们只需要了解IO流实现的原理即可。

### 4.2File类

这个类表示操作系统上的文件或者目录实例，可以用这个类操作文件。

实例语法

~~~java
 File file = new File("D:/IO/text.txt"); //括号内是一个文件的路径
~~~

我们定位文件路径的有两种路径，一种是相对路径，一种是绝对路径。

相对路径：是指对于当前位置的路径。

绝对路径：是磁盘上完整的路径。

通过以上实例化语句，我们可以通过file来操作"D:/IO/text.txt"文件。

~~~java
file.isFile()；//判断是否为文件，返回值为布尔类型
    
file.isDirectory()//判断是否为文件夹（目录），返回值为布尔类型

file.getAbsolutePath()//取得文件绝对路径

file.delete()//删除该文件
~~~

File类的操作还有很多，这里不一一列举，可以查看API文档了解。

### 4.3字节流

字节抽象类 InputStream ：字节输⼊流 ，可理解为把数据读入Java内

public int read(){}。

 public int read(byte[] b){}。

 public int read(byte[] b,int off,int len){}。

 OutputStream ：字节输出流 ，可理解为把数据从java中写成文档

public void write(int n){}。 

public void write(byte[] b){}。 

public void write(byte[] b,int off,int len){}。 

可看实例

~~~java
 public static void main(String[] args) {
        copy("D:/IO/text.txt","D:/IO/copytext.txt");
    }
    static void copy(String src,String dest) {

        try (
            InputStream input = new FileInputStream(src);
            OutputStream output = new FileOutputStream(dest);
        )
            {
            byte[] b = new byte[1024];
            int len;
            while ((len = input.read(b)) != -1) {
                output.write(b, 0, len);
            }
        } catch (FileNotFoundException e) {
            e.printStackTrace();
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
~~~

IO流多余不再赘述。

















