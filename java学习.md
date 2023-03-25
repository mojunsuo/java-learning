# java学习

![](D:\Typora\image\QQ图片20230321123306.png)

## 基础语法知识

```java
LinkedList<Integer>b=new LinkedList<Integer>();
b.add(0);
b.add(1);
int c=b.getLast();
b.removeLast();

ArrayList<Integer>a=new ArrayList<Integer>(Arrays.asList(0,1));

那么问题来了，我们为什么不直接使用 ArrayList list=newArrayList();的方式来实例化ArrayList对象，并调用其中的方法，而有时候大部分会通过List list=new ArrayList();来实例化对象呢？
原因有二：
第一，两种实例化的方式由所区别，第一种方式创建的对象继承了ArrayList的所有属性和方法。 而第二种方式创建的对象只能调用List接口中的方法，不能调用ArrayList中的方法。
第二、使用第二种方式创建的对象更为方便。List接口有多个实现类，现在用的是ArrayList，如果要将其更换成其它的实现类，如 LinkedList或者Vector等等，这时只需要改变这一行就行了： List list = new LinkedList(); 其它使用了list地方的代码根本不需要改动。 在编写代码时，较为方便。
    
    List<List<Integer>>ans=new ArrayList();
    LinkedList<Integer>b=new LinkedList<Integer>();
    //List<Integer>c=new ArrayList<Integer>(b);(可以的)
    ans.add(b);

实现固定大小的ArrayList，就是先添加到这个大小就行
	edges = new ArrayList<List<Integer>>();
        for (int i = 0; i < numCourses; ++i) {
            edges.add(new ArrayList<Integer>());
        }



    public int Sort() {
        String str = "abcutvznkzojbyuiodef";
        //字符串变成字符数组
        char[] arr = str.toCharArray();
        //排序
        Arrays.sort(arr);
        //排序后变成字符串
        String newStr = new String(arr);
        System.out.println(newStr);
        return 0;
    }

String b="hello";
StringBuffer a=new StringBuffer(b);
String c=new String(a);

普通队列
Queue<Integer>a=new LinkedList<Integer>();
a.add(0);
int b=a.peek();
a.remove();
a.isEmpty();

双端队列
Deque<Integer> stack = new LinkedList<Integer>();
stack.addLast();
stack.removeLast();

优先队列
	PriorityQueue<Integer> queMin;
    PriorityQueue<Integer> queMax;

    public MedianFinder() {
        queMin = new PriorityQueue<Integer>((a, b) -> {
            return b-a;
        });
        queMax = new PriorityQueue<Integer>((a, b) -> (a - b));
    }
Queue<Integer>que = new PriorityQueue<>((x1,x2)->{return x2-x1;});
que.add(2);
que.add(1);
que.add(3);
//此时队列中的元素依次为3,2,1
class Solution {
    class Status implements Comparable<Status> {
        // 某个节点的数值与指针
        int val;
        ListNode ptr;
        // 构造函数
        public Status(int val, ListNode ptr) {
            this.val = val;
            this.ptr = ptr;
        }
        // 在优先队列里面，以升序排列
        public int compareTo(Status status2) {
            return this.val - status2.val;
        }
    }
    public ListNode mergeKLists(ListNode[] lists) {
        // 创建优先队列
        PriorityQueue<Status> queue = new PriorityQueue<>();
        ListNode pre = new ListNode(0);
        ListNode preHead = pre;
        // 我们需要维护当前每个链表没有被合并的元素的最前面一个，k 个链表就最多有 k 个满足这样条件的元素，每次在这些元素里面选取 val 属性最小的元素合并到答案中。在选取最小元素的时候，我们可以用优先队列来优化这个过程。
        for (ListNode node : lists) {
            if (node != null) {
                queue.offer(new Status(node.val, node));//!!!!
            }
        }


根据需要初始化的目标选用，初始化以后就只需要知道他其实相当于左边那个类，就不用管了，只用左边那个类的方法写
    
sort用Collecions可以自定义排序
Collections.sort(array,(a,b)->{
    return a-b;
})
或者a.sort((o1,o2)->{
    return o2-o1;
    //返回值为1表示交换，要降序排序，o1<o2时交换，o2-o1>0，return o2-o1;
})
    
    
遍历哈希表
    for(Map.Entry<String,String>entry:mp.entrySet())
    {
        String a=entry.getKey();
        String b=entry.getValue();
    }

整数转换成字符串:String str=""+num;
字符串转换成整数:Integer.parseInt(str),Long.parseLong(str);
截取子串:System.out.println(Str.substring(4) );从start位置截取，可指定末尾，可不指定
截取一个范围内的，记住是开区间，末尾取不了
int转换成char,char a=(char)(b+'0');
比较两个字符串字典序，compareTo,若a.compareTo(b)小于0则表示a更小
String获取某个位置字符，charAt，但若要修改，要先写成toCharArray()，然后改
StringBuffer也是用length()获取长度，charAt获取某个位置，deleteCharAt删除，substring截取
    
java实现函数：传参就行
    
字典树:
class Trie {
    private Trie[] children;
    private boolean isEnd;

    public Trie() {
        children = new Trie[26];
        isEnd = false;
    }
    
    public void insert(String word) {
        Trie node = this;
        for (int i = 0; i < word.length(); i++) {
            char ch = word.charAt(i);
            int index = ch - 'a';
            if (node.children[index] == null) {
                node.children[index] = new Trie();
            }
            node = node.children[index];
        }
        node.isEnd = true;
    }
    
    public boolean search(String word) {
        Trie node = searchPrefix(word);
        return node != null && node.isEnd;
    }
    
    public boolean startsWith(String prefix) {
        return searchPrefix(prefix) != null;
    }

    private Trie searchPrefix(String prefix) {
        Trie node = this;
        for (int i = 0; i < prefix.length(); i++) {
            char ch = prefix.charAt(i);
            int index = ch - 'a';
            if (node.children[index] == null) {
                return null;
            }
            node = node.children[index];
        }
        return node;
    }
}

class Solution {
    class TrieNode {
        String s;
        TrieNode[] tns = new TrieNode[26];
    }
    void insert(String s) {
        TrieNode p = root;
        for (int i = 0; i < s.length(); i++) {
            int u = s.charAt(i) - 'a';
            if (p.tns[u] == null) p.tns[u] = new TrieNode();
            p = p.tns[u];
        }
        p.s = s;
    }
    Set<String> set = new HashSet<>();
    char[][] board;
    int n, m;
    TrieNode root = new TrieNode();
    int[][] dirs = new int[][]{{1,0},{-1,0},{0,1},{0,-1}};
    boolean[][] vis = new boolean[15][15];
    public List<String> findWords(char[][] _board, String[] words) {
        board = _board;
        m = board.length; n = board[0].length;
        for (String w : words) insert(w);
        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                int u = board[i][j] - 'a';
                if (root.tns[u] != null) {
                    vis[i][j] = true;
                    dfs(i, j, root.tns[u]);
                    vis[i][j] = false;
                }
            }
        }
        List<String> ans = new ArrayList<>();
        for (String s : set) ans.add(s);
        return ans;
    }
    void dfs(int i, int j, TrieNode node) {
        if (node.s != null) set.add(node.s);
        for (int[] d : dirs) {
            int dx = i + d[0], dy = j + d[1];
            if (dx < 0 || dx >= m || dy < 0 || dy >= n) continue;
            if (vis[dx][dy]) continue;
            int u = board[dx][dy] - 'a';
            if (node.tns[u] != null) {
                vis[dx][dy] = true;
                dfs(dx, dy, node.tns[u]);
                vis[dx][dy] = false;
            }
        }
    }
}

c++字典树
struct Trie {
    unordered_map<string, Trie *> children;
    int weight;
};

class WordFilter {
public:
    Trie *trie=new Trie();
    WordFilter(vector<string>& words) {
    }
    insert,search等等
        
        
c++和java的class和struct都可以放在内部，放在外部用this，放在内部用全局变量。
        
java输入输出：
import java.io.*;
import java.util.*;

public class Main {
    public static void main(String args[]) throws Exception {
        Scanner cin=new Scanner(System.in);
        var a = cin.nextInt();
        var b = cin.nextInt();
        System.out.println(a + b);
    }
}
```

归并排序，快速排序，堆排序：https://javaguide.cn/cs-basics/algorithms/10-classical-sorting-algorithms.html#%E4%BB%A3%E7%A0%81%E5%AE%9E%E7%8E%B0-4

![](D:\Typora\image\QQ图片20230316224129.png)



然后看下链表和LRU,数位dp

快捷键以及依赖关系，设计模式，虚拟机，哈希表，秒杀，单例懒汉



## Spring

### IOC和bean的一些知识

Spring中IOC容器的主要表现形式是BeanFactory（父类，功能低级点，算低级容器）和ApplicationContext（子类，功能高级点，算高级容器）这两个接口。这两个接口的具体实现类就可以看成是IOC容器在Spring中的具体体现

spring 的 IOC 负责对象的实例化、对象的初始化、对象和对象之间依赖关系配置、对象的销毁、对外提供对象的查找,对象的整个生命周期都是由容器来控制的。这个 IOC 是一个具有依赖注入功能的 容器。
我们需要的对象都是由 IOC （控制反转）容器进行创建管理的，不需要我们手动去new对象出来，由IOC容器帮我们组装好，我们需要某个对象的时候就去IOC容器里面拿就行了。



使用bean，ctx.getBean(xxx. class)

bean就是一个java对象，只是因为他是由spring创建，容器管理的，所以才叫bean，给控制层（表现层），业务层，数据层（@Repository）全部加上注解@Component，@Controller...同时给SpringConfig类加上注解@ComponentScan，@Configuration...

创建的时候，AnnotationConfigApplicationContext(SpringConfig.class) 再对业务层的变量（对象或者常量）进行注入，引用注入AutoWired将会按接口名字进行对象注入（注入的是接口，接口必须要有一个实现类，对，有两个就按名字注入，有一个就按类型），普通注入就直接@Value("")，也可以花括号@Value(${})，在springConfig上加PropertySource引进其他数据，再用其他数据的名字进行注入也可。大驼峰命名给首字母也大写。（平时的库函数是首字母不大写，后面遇到别的单词，首字母大写）,JdbcConfig数据配置类,用@Bean配置第三方bean，然后进行一堆创建，可以直接在方法上接受形参，接受的形参会被自动装配。在SpringConfig上写@Import(JdbcConfig.class)，多个对象可以使用大括号

![](D:\Typora\image\QQ图片20230320212428.png)





### spring整合mybatis

Mybatis内部对原生对象进行加强处理得到一个对应的代理对象，我们通过当前对象方法调用进行数据库操作时，实质是Mybatis内部生成的代理对象内部的统一方法在进行工作。
举例，我们通过UserMapper接口声明一个userMapper对象，Mybatis内部验证发现userMapper对象被mapper注解修饰，因此对该userMapper对象进行加强处理得到一个对应的代理对象，也就是我们真正拿到的userMapper对象是一个代理对象。后续在通过userMapper调用selectAll方法时，Mybatis内部对其进行拦截，统一执行内部的invoke方法，真正实现JDBC操作的过程是通过invoke方法实现的。

![](D:\Typora\image\QQ图片20230320222643.png)

![](D:\Typora\image\QQ图片20230320222934.png)



### spring整合Junit测试单元

![](D:\Typora\image\QQ图片20230320223358.png)



### AOP：在不惊动原始设计的基础上增强功能，代理模式

![](D:\Typora\image\QQ图片20230320225755.png)

![](D:\Typora\image\QQ图片20230320230749.png)

![](D:\Typora\image\QQ图片20230320230758.png)

![](D:\Typora\image\QQ图片20230320231322.png)

![](D:\Typora\image\QQ图片20230320232001.png)

*必有  ..不一定

![](D:\Typora\image\QQ图片20230321100843.png)

![](D:\Typora\image\QQ图片20230321105521.png)

![](D:\Typora\image\QQ图片20230321105524.png)

![](D:\Typora\image\QQ图片20230321110537.png)



### spring事务

![](D:\Typora\image\QQ图片20230321115759.png)

![](D:\Typora\image\QQ图片20230321115803.png)

![](D:\Typora\image\QQ图片20230321115807.png)

![](D:\Typora\image\QQ图片20230321122339.png)



### SpringMVC

![](D:\Typora\image\QQ图片20230321144033.png)

![](D:\Typora\image\QQ图片20230321144036.png)

![](D:\Typora\image\QQ图片20230321144038.png)

![](D:\Typora\image\QQ图片20230321144040.png)



把spring和springMVC环境都加载

![](D:\Typora\image\QQ图片20230321162029.png)

更简单的方式

![](D:\Typora\image\QQ图片20230321162210.png)

@EnableWebMvc开启支持

发送请求用APIpost，很多都能发，传数据，数组都行，非json（请求路径，form表单）记住@RequestParam

json@RequestBody 主流



### REST风格

![](D:\Typora\image\QQ图片20230321200748.png)

![](D:\Typora\image\QQ图片20230321200816.png)

![](D:\Typora\image\QQ图片20230321202240.png)

![](D:\Typora\image\QQ图片20230321202244.png)

![](D:\Typora\image\QQ图片20230321210919.png)

![](D:\Typora\image\QQ图片20230321210934.png)

post:发起请求的人要新建信息

get:发起请求的人要从后端获取信息

注意看看前端实现，表格等



### SSM整合

#### SSM整合流程

![](D:\Typora\image\QQ图片20230322110803.png)



#### 表现层数据封装

![](D:\Typora\image\QQ图片20230321224338.png)

![](D:\Typora\image\QQ图片20230321224341.png)



#### 异常处理

![](D:\Typora\image\QQ图片20230321224343.png)

![](D:\Typora\image\QQ图片20230321224644.png)

![](D:\Typora\image\QQ图片20230321224647.png)

![](D:\Typora\image\QQ图片20230321224650.png)

![](D:\Typora\image\QQ图片20230321224652.png)

#### SSM前后台协议

![](D:\Typora\image\QQ图片20230322111338.png)

![](D:\Typora\image\QQ图片20230322111340.png)

![](D:\Typora\image\QQ图片20230322111342.png)

![](D:\Typora\image\QQ图片20230322111344.png)

![](D:\Typora\image\QQ图片20230322111347.png)

#### 拦截器

![](D:\Typora\image\QQ图片20230322153313.png)

![](D:\Typora\image\QQ图片20230322153316.png)

![](D:\Typora\image\QQ图片20230322153319.png)

![](D:\Typora\image\QQ图片20230322153322.png)

![](D:\Typora\image\QQ图片20230322153328.png)

![](D:\Typora\image\QQ图片20230322153330.png)

## Maven

### maven的各类关系

依赖：即需要用到

聚合：多个模块服务于当前模块，在当前模块中定义，能感知哪个分模块出错

继承：子继承父，父中定义默认和可选的配置，子类继承默认配置的同时，根据需求继承可选配置

![](D:\Typora\image\QQ图片20230322153423.png)

### maven的属性配置及使用

![](D:\Typora\image\QQ图片20230322155445.png)

![](D:\Typora\image\QQ图片20230322155447.png)

![](D:\Typora\image\QQ图片20230322155449.png)

![](D:\Typora\image\QQ图片20230322155451.png)

### maven多环境

![](D:\Typora\image\QQ图片20230322161332.png)

跳过测试：mvn 指令（比如install） -D skipTests

### maven私服资源上传与下载

![](D:\Typora\image\QQ图片20230322165512.png)

![](D:\Typora\image\QQ图片20230322165516.png)

![](D:\Typora\image\QQ图片20230322165518.png)

## SpringBoot

### Spring和SpringBoot对比

![](D:\Typora\image\QQ图片20230323163039.png)

### yaml数据读取三种方式

![](D:\Typora\image\QQ图片20230322214738.png)

![](D:\Typora\image\QQ图片20230322214740.png)

![](D:\Typora\image\QQ图片20230322214743.png)

### 多环境启动

![](D:\Typora\image\QQ图片20230322222543-1679495777234.png)

![](D:\Typora\image\QQ图片20230322222545-1679495800626.png)

### SpringBoot整合Junit

![](D:\Typora\image\QQ图片20230322224414.png)

### Spring整合Mybatis

![](D:\Typora\image\QQ图片20230322224538.png)

![](D:\Typora\image\QQ图片20230322225432.png)

![](D:\Typora\image\QQ图片20230322225358.png)

![](D:\Typora\image\QQ图片20230322225401.png)

### 基于SpringBoot的SSM整合案例

![](D:\Typora\image\QQ图片20230322225537.png)



### SpringBoot整合MyBatisPlus

![](D:\Typora\image\QQ图片20230323160705.png)

![](D:\Typora\image\QQ图片20230323160707.png)

![](D:\Typora\image\QQ图片20230323160710.png)

![](D:\Typora\image\QQ图片20230323160714.png)

### 标准CRUD制作

![](D:\Typora\image\QQ图片20230323162741.png)

![](D:\Typora\image\QQ图片20230323162744.png)

![](D:\Typora\image\QQ图片20230323162747.png)

### 标准分页功能

![](D:\Typora\image\QQ图片20230323165236.png)

![](D:\Typora\image\QQ图片20230323165239.png)

### 条件查询

![](D:\Typora\image\QQ图片20230323171029.png)

### 条件查询Null值判定

用户可能对空白的部分，不写就直接查询添加，这种操作是不行 

![](D:\Typora\image\QQ图片20230323173501.png)

### 查询条件设置

![](D:\Typora\image\QQ图片20230323194844.png)

![](D:\Typora\image\QQ图片20230323195850.png)

![](D:\Typora\image\QQ图片20230323195853.png)

### 全局配置

![](D:\Typora\image\QQ图片20230323204140.png)

### 多数据操作

![](D:\Typora\image\QQ图片20230323204406.png)

### 逻辑删除

删了，但可能还是想看到被删的数据，所以有这个需求

![](D:\Typora\image\QQ图片20230323205736.png)



### 代码生成器

![](D:\Typora\image\QQ图片20230323213309.png)

![](D:\Typora\image\QQ图片20230323213311.png)

![](D:\Typora\image\QQ图片20230323213314.png)

![](D:\Typora\image\QQ图片20230323213316.png)

![](D:\Typora\image\QQ图片20230323213320.png)