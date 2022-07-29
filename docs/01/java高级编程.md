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

### 4.4序列化IO

```
序列化，就是把一个引用类型，拆分成最小的单位(byte)，以便今后数据字节流的形式存储在磁盘中或者是通过网络协议发送另一方，它是数据存储和发送的一种重要技术
```

```
 public static void main(String[] args) {
//        Person[] arr = new Person[]{new Person("a"), new Person("b"), new Person("c"),};
//
//        change(arr);
        Person p1 = new Person("Jack");
        System.out.println(p1.hashCode());
        serializable(p1);

        unSerializable();
    }

    // 建一个对象的数据拆分成字节，有序的写入到文件中去
    private static void serializable(Person p1) {
        Path path = Paths.get("c:/Users/ThinkAboutAI/Desktop/person.data");
        try ( // 只要实现了Closeable接口的实例都会自动关闭
              OutputStream out = Files.newOutputStream(path);
              ObjectOutputStream oos = new ObjectOutputStream(out)
        ) {
            oos.writeObject(p1);
        } catch (IOException e) {
            e.printStackTrace();
        }
    }

    private static void unSerializable() {
        try (
                ObjectInputStream ois = new ObjectInputStream(Files.newInputStream(Paths.get("c:/Users/ThinkAboutAI/Desktop/person.data")))
        ) {
            Object obj = ois.readObject();
            if (obj instanceof Person) {
                Person person = (Person) obj;
                System.out.println(person.hashCode());
                System.out.println(person);
            }
        } catch (IOException e) {
            e.printStackTrace();
        } catch (ClassNotFoundException e) {
            throw new RuntimeException(e);
        }
    }

    private static void change(Person[] arr) {
        arr[0].name = "x";
    }


}

/**
 * <p>需要被序列化的类一定要实现java.io.Serializable接口：因为ObjectOutputStream在序列化的时候，会有一个类型检测</p>
 * <p>serialVersionUID相当于一个防伪编码，作用是为了在序列化与反序列化的过程中，预防有人篡改字节码中的信息</p>
 */
class Person implements Serializable {

    private static final long serialVersionUID = 2263583963027808782L; // 声明这个类的实例是可以被序列化的

    // JVM在反序列化的时候，会去识别这个“防伪编码”，作用有点类似于MD5校验
//    private static final long serialVersionUID = 1L;

    String name;

    @Override
    public String toString() {
        return "Person{" +
                "name='" + name + '\'' +
                '}';
    }

    public Person(String name) {
        this.name = name;
    }
```

IO知识点理解过程即可，后续开发将会使用各种框架代替。这里只列举少许示例。

## 5、网络编程

后续开发同样会用框架代替，知识了解、代码理解即可

### 5.1网络

在学习Java网络编程之前，我们先来了解什么是计算机网络。

计算机网络是指两台或更多的计算机组成的网络，在同一个网络中，任意两台计算机都可以直接通信，因为所有计算机都需要遵循同一种网络协议。

那什么是互联网呢？互联网是网络的网络（internet），即把很多计算机网络连接起来，形成一个全球统一的互联网。

对某个特定的计算机网络来说，它可能使用网络协议ABC，而另一个计算机网络可能使用网络协议XYZ。如果计算机网络各自的通讯协议不统一，就没法把不同的网络连接起来形成互联网。因此，为了把计算机网络接入互联网，就必须使用TCP/IP协议。

TCP/IP协议泛指互联网协议，其中最重要的两个协议是TCP协议和IP协议。只有使用TCP/IP协议的计算机才能够联入互联网，使用其他网络协议（例如NetBIOS、AppleTalk协议等）是无法联入互联网的。

### 5.2 IP地址

在互联网中，一个IP地址用于唯一标识一个网络接口（Network Interface）。一台联入互联网的计算机肯定有一个IP地址，但也可能有多个IP地址。

IP地址分为IPv4和IPv6两种。IPv4采用32位地址，类似`101.202.99.12`，而IPv6采用128位地址，类似`2001:0DA8:100A:0000:0000:1020:F2F3:1428`。IPv4地址总共有2^32个（大约42亿），而IPv6地址则总共有2^128个（大约340万亿亿亿亿），IPv4的地址目前已耗尽，而IPv6的地址是根本用不完的。

IP地址又分为公网IP地址和内网IP地址。公网IP地址可以直接被访问，内网IP地址只能在内网访问。内网IP地址类似于：

- 192.168.x.x
- 10.x.x.x

有一个特殊的IP地址，称之为本机地址，它总是`127.0.0.1`。

IPv4地址实际上是一个32位整数。例如：

```ascii
106717964 = 0x65ca630c
          = 65  ca  63 0c
          = 101.202.99.12
```

如果一台计算机只有一个网卡，并且接入了网络，那么，它有一个本机地址`127.0.0.1`，还有一个IP地址，例如`101.202.99.12`，可以通过这个IP地址接入网络。

如果一台计算机有两块网卡，那么除了本机地址，它可以有两个IP地址，可以分别接入两个网络。通常连接两个网络的设备是路由器或者交换机，它至少有两个IP地址，分别接入不同的网络，让网络之间连接起来。

如果两台计算机位于同一个网络，那么他们之间可以直接通信，因为他们的IP地址前段是相同的，也就是网络号是相同的。网络号是IP地址通过子网掩码过滤后得到的。例如：

某台计算机的IP是`101.202.99.2`，子网掩码是`255.255.255.0`，那么计算该计算机的网络号是：

```
IP = 101.202.99.2
Mask = 255.255.255.0
Network = IP & Mask = 101.202.99.0
```

每台计算机都需要正确配置IP地址和子网掩码，根据这两个就可以计算网络号，如果两台计算机计算出的网络号相同，说明两台计算机在同一个网络，可以直接通信。如果两台计算机计算出的网络号不同，那么两台计算机不在同一个网络，不能直接通信，它们之间必须通过路由器或者交换机这样的网络设备间接通信，我们把这种设备称为网关。

网关的作用就是连接多个网络，负责把来自一个网络的数据包发到另一个网络，这个过程叫路由。

所以，一台计算机的一个网卡会有3个关键配置：

![image-20210817130832261](D:\桌面\rivtto\docs\01\插图\image-20210817130832261.png)

- IP地址，例如：`10.0.2.15`
- 子网掩码，例如：`255.255.255.0`
- 网关的IP地址，例如：`10.0.2.2`

### 5.3 域名

因为直接记忆IP地址非常困难，所以我们通常使用域名访问某个特定的服务。域名解析服务器DNS负责把域名翻译成对应的IP，客户端再根据IP地址访问服务器。

用`nslookup`可以查看域名对应的IP地址：

```
$ nslookup baidu.com
Server:  xxx.xxx.xxx.xxx
Address: xxx.xxx.xxx.xxx#53

Non-authoritative answer:
Name:    www.baidu.com
Address: 47.99.33.223
```

有一个特殊的本机域名`localhost`，它对应的IP地址总是本机地址`127.0.0.1`。

### 5.4 网络模型

由于计算机网络从底层的传输到高层的软件设计十分复杂，要合理地设计计算机网络模型，必须采用分层模型，每一层负责处理自己的操作。OSI（Open System Interconnect）网络模型是ISO组织定义的一个计算机互联的标准模型，注意它只是一个定义，目的是为了简化网络各层的操作，提供标准接口便于实现和维护。这个模型从上到下依次是：

- 应用层，提供应用程序之间的通信；
- 表示层：处理数据格式，加解密等等；
- 会话层：负责建立和维护会话；
- 传输层：负责提供端到端的可靠传输；
- 网络层：负责根据目标地址选择路由来传输数据；
- 链路层和物理层：负责把数据进行分片并且真正通过物理网络传输，例如，无线网、光纤等。

互联网实际使用的TCP/IP模型并不是对应到OSI的7层模型，而是大致对应OSI的5层模型：

| OSI    | TCP/IP     |
| :----- | :--------- |
| 应用层 | 应用层     |
| 表示层 |            |
| 会话层 |            |
| 传输层 | 传输层     |
| 网络层 | IP层       |
| 链路层 | 网络接口层 |
| 物理层 |            |

### 5.5 常用协议

IP协议是一个分组交换，它不保证可靠传输。而TCP协议是传输控制协议，它是面向连接的协议，支持可靠传输和双向通信。TCP协议是建立在IP协议之上的，简单地说，IP协议只负责发数据包，不保证顺序和正确性，而TCP协议负责控制数据包传输，它在传输数据之前需要先建立连接，建立连接后才能传输数据，传输完后还需要断开连接。TCP协议之所以能保证数据的可靠传输，是通过接收确认、超时重传这些机制实现的。并且，TCP协议允许双向通信，即通信双方可以同时发送和接收数据。

TCP协议也是应用最广泛的协议，许多高级协议都是建立在TCP协议之上的，例如HTTP、SMTP等。

UDP协议（User Datagram Protocol）是一种数据报文协议，它是无连接协议，不保证可靠传输。因为UDP协议在通信前不需要建立连接，因此它的传输效率比TCP高，而且UDP协议比TCP协议要简单得多。

选择UDP协议时，传输的数据通常是能容忍丢失的，例如，一些语音视频通信的应用会选择UDP协议。

### 5.6TCP/IP协议编程

~~~java
public class Client {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        try (
                Socket socket = new Socket(InetAddress.getByName("127.0.0.1"),8080);
                OutputStream ops =socket.getOutputStream()
        ){
            System.out.println("开始：");
            while (!(sc.nextLine().equals("q"))){
                String msg = sc.nextLine();
                System.out.println("说些什么:");
                ops.write(msg.getBytes());
            }

        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}

public class ServerProgram {
    public static void main(String[] args) {
        try (
                ServerSocket ss = new ServerSocket(8080);
                Socket socket = ss.accept();
                InputStream ins =socket.getInputStream();
        ) {
            byte[] b = new byte[1024];
            int len ;
            while ((len = ins.read(b)) != -1){
                String msg =new String(b,0,len);
                System.out.println(msg);
            }

        }catch (Exception e){
            e.printStackTrace();
        }
    }
}
// Internet P：每一台硬件（能接入网络的）在网络上的一个唯一地址标识，其它设备能直接通过IP来对该设备发起连接请求
    // Port：端口，这个是为了区分不同的应用程序如何来接受网络数据包

    // Transform verb. 传输
    // Control 控制
    // Protocol 协议

    // 基于双工的网络传输协议
    // 在连接的时候，双方都会有一些前置的交互：你在吗？我在？我能向你发送数据吗？可以？现在可以发送了吗？可以了
    // 因此，这个连接一旦创建好以后，发送的数据，在数据帧上是顺序准确的、数据一定是完整的（丢包）
    // 相对其它的通讯协议来说，发送的效率较慢
    // 连接的两方，是有主次之分的，分为服务器方和客户端方
~~~

### 6.7UDP编程

```
public class Receiver {
    public static void main(String[] args) {
        // 创建数据报文的socket
        try (
                DatagramSocket ds = new DatagramSocket(8080);
        ) {
            byte[] buffer = new byte[1024]; // 1kb
            // 真正用来盛放数据的数据包裹
            DatagramPacket dp = new DatagramPacket(buffer, buffer.length);
            // 当buffer被接收的数据填充满的时候，就会return
            ds.receive(dp); // 当没有接收到消息的时候，会一直阻塞

            // 服务器端是可以获取到客户端的地址信息
//            dp.getAddress(); // 获取对方IP
//            dp.getPort(); // 获取端口

            int len = dp.getLength(); // 真正的接收到数据的长度
            byte[] data = dp.getData(); // 它的长度与buffer的长度是一样
            String msg = new String(data, 0, len);
            System.out.println(msg);
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}

public class Sender {
    public static void main(String[] args) {
        try (
                DatagramSocket socket = new DatagramSocket()
        ) {
            byte[] msg = "hello world".getBytes();
            // 在发送的数据报文中，封装目标的地址信息
            DatagramPacket dp = new DatagramPacket(msg, msg.length, InetAddress.getByName("127.0.0.1"), 8080);
            // while
            socket.send(dp);

            // 发送的数据传输完毕的时候，发送一个类似于Q的表示
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}

```

## 6、多线程

### 6.1进程与线程与cpu

进程：进程是程序运行的实例，程序是由一个或者多个进程组成，进程包含该程序的资源和数据，并且占据一定的内存空间。操作系统可以同时进行多个进程。

线程：指的是由多个指令组成的一条序列，可以理解为是进程中的一条指令序列，多个线程可以同时处理（实际上还是一次一个，只是交替速度很快）

CPU：是电脑的“大脑”，所有指令由他处理，才可以继续运行，但是一次只能处理一个，每次处理很短的时间，就会换成下一个程序，以此循环，交替速度非常快，在使用者看来，就是程序同时运行，线程会争夺cpu的处理时间片。



### 6.2线程的操作

#### 6.2.1创建

线程的创建有（常用）两种方法（也可以说3种，第三种是第二种的lambda表达式拓展）。

PS：所有的线程都是由Thread类启动。

一是继承Thread类，重写run方法

~~~java
lass MyThread extends Thread{
    public void run(){
        for (int i = 0; i < 50; i++) {
            System.out.println(Thread.currentThread().getName()+"-"+i);
            try {
                Thread.sleep(100);
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        }
    }
}

   public static void main(String[] args) {
        MyThread mt = new MyThread();
        mt.start();
~~~

start方法表示启动线程。



二是实现Runnable接口，实现run方法：、

~~~java
class MyRunnable implements Runnable{

    @Override
    public void run() {
        for (int i = 0; i < 50; i++) {
            System.out.println(Thread.currentThread().getName()+"-"+i);
            try {
                Thread.sleep(100);
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        }
    }
}

 MyRunnable mt2 = new MyRunnable();
        Thread td = new Thread(mt2);
        td.start();
~~~

由以上代码可见，最后的代码运行，还是由Thread类实现，实例化Thread对象时，传入一个实现Runnable接口的对象参数。



方法的选择：一般我们使用第二种方式，因为第一种方式是继承关系，而java中只能单根继承，从而会使得代码复用性降低。所以实现Runnable接口，更加灵活。



#### 6.2.2线程的暂停(休眠)

当我们需要当前线程停下一段时间，或者需要等待其他线程先结束时，我们就需要手动暂停一下该线程，我们用Thread.sleep    来实现该线程的暂停（休眠）

~~~java
 try {
                Thread.sleep(100);//表示休眠100毫秒
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
~~~

因为休眠方法声明在JDK里面有抛出异常标识，所以我们需要处理一下。

#### 6.2.3join方法

join可以译为等待加入的意思，是指在某一条线程调用另一条线程的join方法，那么该线程就会等待加入的方法执行完毕。

例如:我们在main方法中加入t.join , 那么main方法必须等到t线程执行结束才会执行后续语句。

~~~java
public class ThreadJoin {
    public static void main(String[] args) {
        Thread t = new Thread(new ThreadJoin);
        System.out.println("开始");
        t.start;
        t.join;
        System.out.println("结束");

class ThreadJoin3 implements Runnable{
    public void run(){
        for (int i = 0; i < 50; i++) {
            System.out.println(Thread.currentThread().getName()+"--"+i);
            try {
                Thread.sleep(100);
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        }
    }
}
~~~

运行以上代码，我们会发现t线程结束，才会打印出结束二字，但是如果没有t.join，那么t线程还没有运行完，主线程就已经结束了，但是t线程也被迫结束。

此例我们可以详细了解join方法的用处。

同时我们会发现join方法中可以传入参数，这个参数是等待时间，以刚才的例子解释

就是t.join（300）,就是主线程等待t线程300毫秒。





#### 6.2.4interrupt方法

当线程执行过程中，需要停止线程时即可





























