### cmd指令

#### 编译：javac 文件名（注意：需要带后缀名）

#### 运行：java 文件名

javac Hello.java

会编译出一个Hello.class文件

再cmd javac Hello

就会运行Hello.class文件



文件名必须和类名名字一致

### 编译型语言和解释型语言

语言分为解释型和编译型，java两者都属于

js属于解释型。编译型就是把一本书翻译完，解释型就是看到哪翻译哪。操作系统属于编译型

### IDE 集成开发环境

intergrated development enviroment

一般包括编辑器，编译器，调试器，图形用户界面等工具

### 常量

#### 整形

1. byte 一个字节 （1字节=8bit）
2. short 2字节
3. int 4字节
4. long 8字节

#### 浮点型

1. float 4字节
2. double 8字节

float的范围比long还要打



整形默认是int 小数默认是double



#### 字符型char

通常使用一个'',内部只能写一个字符

为什么通常呢？因为可以这样写：

char c1='\0043' 这里面是一个值，其实也代表一个字符

char c2=97  这样也是可以的

1字符=2字节



```java
char c3=5;
char c4='5'
int i1=(int)c4;
//c4对应5的ascii值 c3表示的5就是ascii值为5
System.out.println(i1)//53
```

变量两种命名方法：

1. int i1=5;
2. 
   1. int i2;
   2. i2=6;



String s1=123//不可以这样写

String是引用数据类型



取余之后得到结果的正负和被取余数的正负号相同



### 一元运算符 ++ --

int a=3;

//b是3 先赋值 后自增

b=a++;

//c是5先自增 后赋值

c=++a;

表示2的3次方

Math.pow(2,3)

### 包package的机制

包就相当于文件夹，防止重名，一般使用公司的域名作为包名：www.baidu.com 那么包名就是 com.baidu.www

并且java class文件的第一句话必须是 package com.baidu.www  

import  com.baidu.*就表示引入baidu文件夹下的所有文件

### javadoc

用来生成自己API文档

参数信息

1. @author
2. @version
3. @since 指明需要最早使用的jdk版本
4. params参数名
5. return返回值情况
6. throws异常抛出情况

案例：

```java
public class demo1 {
    public static void main(String[] args) {
        /**
         * @author carlos
         * @version 1.0
         */
    }
}

```

javadoc -encoding UTF-8 -charset UTF-8 文件名.java

生成一个文件夹 其中index.html打开就是项目解释

### next和nextLine方法

1. next()要有有效字符后才可以结束 比如输入wo shi只会接收到 wo
2. nextLine()以enter符号为结束符 输入wo shi1接收wo shi

scanner案例：

```java
package scanner;

import java.util.Scanner;

public class scanner {
    public static void main(String[] args) {
//        创建一个扫描器对象，用于接收键盘数据
        Scanner myscanner = new Scanner(System.in);
        System.out.println("使用方式接受：");
//        判断用户是否输入
        if (myscanner.hasNext()) {
//            使用nextLine接受
            String str1 = myscanner.nextLine();
            System.out.println("输入的内容为" + str1);
        }
//        所有IO流的类如果不关闭会一直占用资源，所以要关闭
        myscanner.close();
    }
}

```

\t表示回车

void表示没有返回值



### idea小技巧

1. IDEA可以按住ctrl键和鼠标右键可以跳转**信息来源地址**

2. ctrl+enter可以查看**错误提示**

3. 格式化代码：在菜单栏中点击【Code】>【Reformat Code】快捷键【Ctrl】+【Alt】+【L】

4. person.name.sout快捷输出person.name

5. alt+insert生成构造器 OK就是有参数，select none就是无参数构造器

6. cmd可以加在路径前面直接写 比如cmd D:\

7. for循环快速简写：9.for 回车

8. **删除光标所在行代码** idea快捷键： Ctrl+X

9. 格式化代码 idea：先Ctrl+A选择全部代码 然后 Ctrl+Alt+L

10. **下上移动正行代码**
      idea：Shift+Ctrl+上下键

11. Shift+Enter，向下插入新行

12. 向下复制整行

    聚焦到要赋值的当前行，直接按住Ctrl + D

13. 具体：

    ```html
    Ctrl+Shift + Enter，语句完成
    “！”，否定完成，输入表达式时按 “！”键
    Ctrl+E，最近的文件
    Ctrl+Shift+E，最近更改的文件
    Shift+Click，可以关闭文件
    Ctrl+[ OR ]，可以跑到大括号的开头与结尾
    Ctrl+F12，可以显示当前文件的结构
    Ctrl+F7，可以查询当前元素在当前文件中的引用，然后按 F3 可以选择
    Ctrl+N，可以快速打开类
    Ctrl+Shift+N，可以快速打开文件
    Alt+Q，可以看到当前方法的声明
    Ctrl+P，可以显示参数信息
    Ctrl+Shift+Insert，可以选择剪贴板内容并插入
    Alt+Insert，可以生成构造器/Getter/Setter等
    Ctrl+Alt+V，可以引入变量。例如：new String(); 自动导入变量定义
    Ctrl+Alt+T，可以把代码包在一个块内，例如：try/catch
    Ctrl+Enter，导入包，自动修正
    Ctrl+Alt+L，格式化代码
    Ctrl+Alt+I，将选中的代码进行自动缩进编排，这个功能在编辑 JSP 文件时也可以工作
    Ctrl+Alt+O，优化导入的类和包
    Ctrl+R，替换文本
    Ctrl+F，查找文本
    Ctrl+Shift+Space，自动补全代码
    Ctrl+空格，代码提示（与系统输入法快捷键冲突）
    Ctrl+Shift+Alt+N，查找类中的方法或变量
    Alt+Shift+C，最近的更改
    Alt+Shift+Up/Down，上/下移一行
    Shift+F6，重构 – 重命名
    Ctrl+X，删除行
    Ctrl+D，复制行
    Ctrl+/或Ctrl+Shift+/，注释（//或者/**/）
    Ctrl+J，自动代码（例如：serr）
    Ctrl+Alt+J，用动态模板环绕
    Ctrl+H，显示类结构图（类的继承层次）
    Ctrl+Q，显示注释文档
    Alt+F1，查找代码所在位置
    Alt+1，快速打开或隐藏工程面板
    Ctrl+Alt+left/right，返回至上次浏览的位置
    Alt+left/right，切换代码视图
    Alt+Up/Down，在方法间快速移动定位
    Ctrl+Shift+Up/Down，向上/下移动语句
    F2 或 Shift+F2，高亮错误或警告快速定位
    Tab，代码标签输入完成后，按 Tab，生成代码
    Ctrl+Shift+F7，高亮显示所有该文本，按 Esc 高亮消失
    Alt+F3，逐个往下查找相同文本，并高亮显示
    Ctrl+Up/Down，光标中转到第一行或最后一行下
    Ctrl+B/Ctrl+Click，快速打开光标处的类或方法（跳转到定义处）
    Ctrl+Alt+B，跳转到方法实现处
    Ctrl+Shift+Backspace，跳转到上次编辑的地方
    Ctrl+O，重写方法
    Ctrl+Alt+Space，类名自动完成
    Ctrl+Alt+Up/Down，快速跳转搜索结果
    Ctrl+Shift+J，整合两行
    Alt+F8，计算变量值
    Ctrl+Shift+V，可以将最近使用的剪贴板内容选择插入到文本
    Ctrl+Alt+Shift+V，简单粘贴
    Shift+Esc，不仅可以把焦点移到编辑器上，而且还可以隐藏当前（或最后活动的）工具窗口
    F12，把焦点从编辑器移到最近使用的工具窗口
    Shift+F1，要打开编辑器光标字符处使用的类或者方法 Java 文档的浏览器
    Ctrl+W，可以选择单词继而语句继而行继而函数
    Ctrl+Shift+W，取消选择光标所在词
    Alt+F7，查找整个工程中使用地某一个类、方法或者变量的位置
    Ctrl+I，实现方法
    Ctrl+Shift+U，大小写转化
    Ctrl+Y，删除当前行
    
    
    Shift+Enter，向下插入新行
    psvm/sout，main/System.out.println(); Ctrl+J，查看更多
    Ctrl+Shift+F，全局查找
    Ctrl+F，查找/Shift+F3，向上查找/F3，向下查找
    Ctrl+Shift+S，高级搜索
    Ctrl+U，转到父类
    Ctrl+Alt+S，打开设置对话框
    Alt+Shift+Inert，开启/关闭列选择模式
    Ctrl+Alt+Shift+S，打开当前项目/模块属性
    Ctrl+G，定位行
    Alt+Home，跳转到导航栏
    Ctrl+Enter，上插一行
    Ctrl+Backspace，按单词删除
    Ctrl+”+/-”，当前方法展开、折叠
    Ctrl+Shift+”+/-”，全部展开、折叠
    【调试部分、编译】
    Ctrl+F2，停止
    Alt+Shift+F9，选择 Debug
    Alt+Shift+F10，选择 Run
    Ctrl+Shift+F9，编译
    Ctrl+Shift+F10，运行
    Ctrl+Shift+F8，查看断点
    F8，步过
    F7，步入
    Shift+F7，智能步入
    Shift+F8，步出
    Alt+Shift+F8，强制步过
    Alt+Shift+F7，强制步入
    Alt+F9，运行至光标处
    Ctrl+Alt+F9，强制运行至光标处
    F9，恢复程序
    Alt+F10，定位到断点
    Ctrl+F8，切换行断点
    Ctrl+F9，生成项目
    Alt+1，项目
    Alt+2，收藏
    Alt+6，TODO
    Alt+7，结构
    Ctrl+Shift+C，复制路径
    Ctrl+Alt+Shift+C，复制引用，必须选择类名
    Ctrl+Alt+Y，同步
    Ctrl+~，快速切换方案（界面外观、代码风格、快捷键映射等菜单）
    Shift+F12，还原默认布局
    Ctrl+Shift+F12，隐藏/恢复所有窗口
    Ctrl+F4，关闭
    Ctrl+Shift+F4，关闭活动选项卡
    Ctrl+Tab，转到下一个拆分器
    Ctrl+Shift+Tab，转到上一个拆分器
    【重构】
    Ctrl+Alt+Shift+T，弹出重构菜单
    Shift+F6，重命名
    F6，移动
    F5，复制
    Alt+Delete，安全删除
    Ctrl+Alt+N，内联
    【查找】
    Ctrl+F，查找
    Ctrl+R，替换
    F3，查找下一个
    Shift+F3，查找上一个
    Ctrl+Shift+F，在路径中查找
    Ctrl+Shift+R，在路径中替换
    Ctrl+Shift+S，搜索结构
    Ctrl+Shift+M，替换结构
    Alt+F7，查找用法
    Ctrl+Alt+F7，显示用法
    Ctrl+F7，在文件中查找用法
    Ctrl+Shift+F7，在文件中高亮显示用法
    ```

    



### 位运算

<< 表示*2

```java
>>表示/2
```

### 增强for循环 一种简写的方式

```java
int[] nums={5,10,15,20,25};
//这样省去了下标，jdk1.5之后开始支持，适合打印输出，但是如果操作每一项就不适合了，因为没有下标，你无法找到要具体操作的项，增强for循环只能操作数组里所有的项
for(int i:nums){
    第一项参数就是每一项，第二项表示数组
    System.out.println(i);
}
```

#### 案例 翻转数组方法

```java
public class Reversearr {
    public static void main(String[] args) {
        int[] arr1 = {1, 2, 3, 4, 5};
        printArr(arr1);
        int[] thisReverse = reverse(arr1);
        //直接打印数组，是打印不出来的会乱码
        printArr(thisReverse);
    }

    //打印数组
    public static void printArr(int[] arr) {
        for (int i = 0; i < arr.length; i++) {
            System.out.println(arr[i] + " ");
        }
    }

    //    翻转数组
    public static int[] reverse(int[] arr) {
//        定义一个数组 长度和传进来的相同
        int[] result = new int[arr.length];
        for (int i = 0, j = arr.length - 1; i < arr.length; i++, j--) {
            result[j] = arr[i];
        }
        return result;
    }

}


```



## 方法

String是修饰符，必须和return的值是一个类型，void表示return为空

public String sayHello(){

​	return "hello";

}

形参和实参的类型必须相同

一个类只能有一个public class但是可以有多个class

### 方法重载的原则

1. 方法名字必须一样
2. 参数列表可以不同（个数 或者 类型 或者 参数排列顺序 不同）
3. 方法的返回类型可以相同也可以不同
4. 但是只有返回类型不同不可以完成方法的重载

#### 带参数的cmd命令

D:\demo\javademo\src>java com.carlos.www.Triangle wo shi ni   

com.carlos.www是包名 wo shi ni是传过去的参数

#### 如果不是静态static方法

say()不是静态方法，则需要先实例化

对象类型 对象名=对象值

Student carlos=new Student();

**注意**：静态方法是和class类一同加载的，所以加载时间比较早，非静态方法是在类实例化之后才加载，所以同一个java文件里，静态方法不能调用非静态方法

```java
package com.carlos.www;
必须先new这个class类，再调用里面的方法
public class Demo1 {
    public static void main(String[] args) {
        new Student().say();
    }
}

```



#### 静态初始化

```java
int[]nums={1,2,3}
Man[] mans={new Man(1,1),new Man(2,2)}
```

动态初始化

```java
int[] a=new int[2];
a[0]=1;
a[1]=2;
```

创建二维数组

```java
int[][] arr=new int[11][11];
```



数组的创建：

```java
int[] nums;
//表示有10个元素在这个数组里 没有赋值就会取int默认值0
nums=new int[10];
```



### 可变项参数

JDK1.5开始有的

一个方法只能有一个可变参数，必须是方法的最后一个参数

```java
public static void printMax(double... nums){
    //nums就是一个数组，也是形参
}
```



### 构造器

一个类即使什么都不写，也存在一个方法。也就是说无参数构造器默认就存在

new关键字其实就是在调用构造器，用来初始化值

特点：

1. 和类名相同
2. 没有返回值

有参数构造器和无参数构造器可以同时存在，调用的时候需要注意调用哪一个

Person carlos=new Person();

对象的属性carlos.name

对象的方法carlos.say()

#### 默认值

1. 数字 0或0.0
2. char u0000
3. boolean false
4. 引用 null

## 数组

#### 数组的特点

1. 数组的长度是确定的，一旦被创建，它的长度就不可以改变
   如果越界就会报错 合法区间[0,length-1]
   越界报错：ArrayIndexOutOFBoundsException
2. 数组元素必须类型相同
3. 数组元素可以是基本类型也可以是引用类型
4. 数组变量属于引用类型，数组也可以看成是对象，数组中的每个元素相当于该对象的成员变量。数组本身就是对象，java中对象是在堆中的，因此数组无论保存原始类型还是其他对象类型，数组对象本身是在堆中
5. 数组就是对象，因为他是new出来的

#### 稀疏数组

大部分元素为0，或者是同一个值的时候，就可以用稀疏数组

<img src="imgs\稀疏数组Snipaste_2021-03-09_14-56-08.jpg" style="zoom:50%;" />

```java
package com.carlos.www;

public class xiShu {
    public static void main(String[] args) {
        int[][] arr = new int[11][11];
        arr[1][2] = 1;
        arr[2][1] = 2;
        System.out.println("原始的数组");
        for (int[] ints : arr) {
            for (int anint : ints) {
                System.out.print(anint + "\t");
            }
            System.out.println();
        }
    }
}

```



#### 私有方法

私有方法前面的修饰词private,其他文件new这个对象不可以直接调用它

idea可以用快捷键alt+insert自动生成get,set方法





## 遇到的BUG

1.cmd命令行：错误: 编码GBK的不可映射字符

解决方法：javac Triangle.java -encoding utf-8



#### 死循环：

while(true){循环体}



## maven

1. maven可以管理jar文件
2. 自动下载jar和他的文档，源代码
3. 管理jar之间的依赖，比如a.jar需要b.jar,maven会自动下载b.jar
4. 管理你需要的jar版本
5. 帮你编译程序，把java变异成class
6. 帮你测试你的代码是否正确
7. 帮你打包文件，形成jar文件,或者war文件
8. 帮你部署项目

总而言之，可以帮我们省时省力的处理掉这些费时费力的工作，以提高开发效率



### maven实现功能的步骤

1. 清理，把之前项目编译的东西删除掉，微信的编译代码做准备
2. 编译，把程序源代码编译为执行代码，java-class文件，这个操作是批量的，不同于javac，javac一次只能编译一个文件
3. 测试，maven可以执行测试程序代码，验证你的功能是否正确，同样的,maven可以同时执行多个测试代码，同时测试多个功能
4. 报告，生成测试结果的文件，测试通过没有
5. 打包，把你的项目中所有的class文件，
6. 安装，把5中生成的文件jar,war安装到本机仓库
7. 部署，把程序安装好就可以执行

### maven的核心概念

用好maven必须了解这些：

1. pom:一个文件，名称是pom.xml,pom翻译过来叫做项目对象模型。maven把一个项目当做一个模型使用，控制maven构建项目的**过程**，管理jar依赖
2. 约定的目录结果：目录里面的文件的目录都是规定下来固定的
3. 坐标：一个唯一的字符串，用来表示资源
4. 管理你的项目可以使用jar文件
5. 仓库管理（了解）：资源存放的位置
6. 生命周期：maven工具构建项目的过程
7. 插件和目标：执行maven构建的时候的工具是插件
8. 继承
9. 聚合

#### 用的最广泛地版本maven3.3.9搭配jdk1.8

#### maven安装使用说明：

1. 解压安装包，必须非中文目录

2. 配置环境变量，指定一个M2_HOME名称，路径就是安装的路径

3. M2_HOME加到path之中，这样写：%M2_HOME%\bin

4. 验证，cmd里面执行mvn -v

5. 第四步需要配置JAVA_HOME,指定jdk

   注意:JAVA_HOME配置的环境变量不要加;



前后端项目运行需要配置的东西：

1.后端接口

需要配置一下字符集，以防止乱码。需要配置一下日志的路径配置

```java
<property value="/Users/codesheep/log">
<encoder>
		<charset>UTF-8</charset>
</encode>
```



2.mysql数据库的地址，用户，密码

3.更改一下redis的配置



## 杂项

### 查看JDK版本

1.输入cmd进入dos界面
2.输入java -version，回车



遇到的BUG javac找不到，配置完成后一定要重启cmd



# typora使用教程

\# 标题

\## 二级标题

\> 引用的话

--- ***都是表示分割线 

！[图片名](图片路径)

[超链接名](超链接地址)

#### nginx不可以有中文空格

