[TOC]

# 后端

## 作业分析

通过这些天的，作业呢，还没做出来，还在看Tomcat里面怎么放Java文件

form表单的元素大概有个了解，感觉现在只需要知道怎么把这个服务端做出来，再用服务端接受请求，再用JDBC把接受的信息放进数据库就行了吧

然而，还在学怎么弄出个服务端

我的时间主要是安装和配置花了很多，然后再IDEA中使用JDBC的时候又用不起，然后又去查了很久，好多问题

# Java学习过程

## [1]学习Java语言基础

下载Java核心技术卷一.pdf

<http://www.java1234.com/a/javabook/javabase/2018/0413/10949.html>

* Java常规代码

```Java
public class ###{ //##必须和文件名一致
    public static void(String [] args)
    {
        Scanner in = new Scanner(String in);//输入必须
        
        System.out.println("What's your name?");//输出
        String name = in.nextLine();//将输入的放到name中
        
        System.out.println("Your name is "+name);
    }
} 
```

* 就我们现学的C++来说，Java的循环没怎么变

```java
for (int element : a) 
	{	
    	System.out.println(element)//这个就是打印a中所有元素了
	}//a必须为数组或者一个实现了 Iterable 接口的类对象？？
```

* break使用的不同

```java
//在Java中，break可以直接跳出多重循环（c++中break只能跳出一重循环）
read_data:
while(...)
{
    ...
    for(...)
    {
        ...
        if(...)
            break read_data;//直接跳到上面的分号后面
        ...
    }
}//然而只能跳出，不能跳入语句数组的不同
```

* 数组的不同

```java
int[] a = new int[100];
String[] names = new String[10];
/*全放在堆中
创建数字数组时，初始化都为0
创建boolean数组时，初始化都为false
创建对象数组时，初始化都为null(表示还未存放任何对象)
*/
```

```java
/* 

emmmm,这个看到继承了，看的时候不想写，之后补写吧

*/
```



# 软件安装与配置

## [1]下载JDK并配置环境变量

配置网址<https://blog.csdn.net/wph199505110014/article/details/79254506>

## [2]安装IDEA并配置

配置网址

<https://blog.csdn.net/qq_42303709/article/details/81983208>

## [3]Mysql的安装配置与基本学习

配置网址

<https://www.cnblogs.com/tangyb/p/8971658.html>//这网址给的my.ini需要改一下安装地址，我检查了好久

学习网址

<https://www.cnblogs.com/programmer-tlh/p/5782418.html>

安装可视化数据库软件Navicat

这里出现了连接问题，百度了得到了解决

<https://blog.csdn.net/qq_32448349/article/details/82428696>

### [3.1]Mysql8的坑

这8有毒啊啊啊啊，花了好长时间<https://blog.csdn.net/an20150509/article/details/81807225>

# JDBC学习

<https://study.163.com/course/courseMain.htm?courseId=1005080015&_trace_c_p_k2_=1d815cb7de4a4875b9a967064ee0b71f>

## 初次接触

```java
import java.sql.*;
public class Test {
    //mysql驱动包
    private static final String DRIVER_NAME = "com.mysql.cj.jdbc.Driver";//这com是特定的
    //数据库连接的地址
    private static final String URL = "jdbc:mysql://localhost:3306/yjh?useSSL=false&serverTimezone=UTC&allowPublicKeyRetrieval=true";//mysql8的坑
    //用户名
    private static final String USER_NAME = "root";
    //密码
    private static final String PASSWORD = "**********";

    public static void main(String[] args) throws Exception{
        Class.forName(DRIVER_NAME); //加载驱动
        Connection conn = DriverManager.getConnection(URL, USER_NAME, PASSWORD);//获取数据库连接
        String sql = "INSERT INTO users SET username = 'YJH',money = 100";//mysql语法
        Statement st = conn.createStatement();
        int flag = st.executeUpdate(sql);
        System.out.println(flag);
    }
```

## 增删查改初学

```java
package cn.java.jdbc;

import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.ResultSet;
import java.sql.Statement;

public class Test {
    //mysql驱动包
    private static final String DRIVER_NAME = "com.mysql.cj.jdbc.Driver";//这com是特定的
    //数据库连接的地址
    private static final String URL = "jdbc:mysql://localhost:3306/yjh?useSSL=false&serverTimezone=UTC&allowPublicKeyRetrieval=true";//mysql8的坑
    //用户名
    private static final String USER_NAME = "root";
    //密码
    private static final String PASSWORD = "**********";
    public static void main(String[] args)throws Exception{
//       inputUser();
//       updateUser();
//       deleteUserId();
//       seleteAllUsers();
    }
//增
    public static void inputUser()throws Exception{
        //加载驱动
        Class.forName(DRIVER_NAME);
        //获得连接(Java连接mysql数据库)
        Connection conn = DriverManager.getConnection(URL, USER_NAME, PASSWORD);
        //创建Statement对象，将sql语句装车
        String sql = "INSERT INTO user SET stuName = '小怪兽',javaScore = '60'";
        Statement st = conn.createStatement();
        int flag = st.executeUpdate(sql);
        if (flag>=1) {
            System.out.println("增加成功");
        } else {
            System.out.println("增加失败");
        }
        //释放数据库资源
        st.close();
        conn.close();
    }
//改
    public static void updateUser() throws Exception{
        //加载驱动
        Class.forName("com.mysql.cj.jdbc.Driver");
        //获得连接
        Connection conn = DriverManager.getConnection(URL, USER_NAME, PASSWORD);
        //创建Statement对象
        Statement st = conn.createStatement();
        String sql = "UPDATE user SET stuName = '奥特曼' WHERE id = 1 ";
        int flag  = st.executeUpdate(sql);
        if (flag>=1) {
            System.out.println("修改成功");
        } else {
            System.out.println("修改失败");
            }
        st.close();
        conn.close();
    }
//删
    public static void deleteUserId() throws Exception{
        //加载驱动
        Class.forName(DRIVER_NAME);
        //获得连接(Java连接mysql数据库)
        Connection conn = DriverManager.getConnection(URL, USER_NAME, PASSWORD);
        //创建Statement对象，将sql语句装车
        String sql = "DELETE FROM user WHERE id = 1";
        Statement st = conn.createStatement();
        int flag = st.executeUpdate(sql);
        if (flag>=1) {
            System.out.println("删除成功");
        } else {
            System.out.println("删除失败");
        }
        //释放数据库资源
        st.close();
        conn.close();

    }
//查
    public static void seleteAllUsers() throws Exception{
    //加载驱动
    Class.forName(DRIVER_NAME);
    //获得连接(Java连接mysql数据库)
    Connection conn = DriverManager.getConnection(URL, USER_NAME, PASSWORD);
    //创建Statement对象，将sql语句装车
    String sql = "SELECT * FROM user";//String sql = "SELECT stuName FROM user"
    Statement st = conn.createStatement();
    //获得查询结果
    ResultSet rs = st.executeQuery(sql);//增删改都是用的executeUpdate(String url)
    //遍历出ResultSet中所有数据记录
    while(rs.next())
    {
        //获取某一条数据的id;
        long id = rs.getLong("id");
        //获取某一条数据的stuName;
        String stuName = rs.getString("stuName");
        //获取某一条数据的javaScore;
        float javaScore = rs.getFloat("javaScore");
        System.out.println(id + "\t"+stuName + "\t"+javaScore );
        //Thread.sleep(1000);
    }
    //释放数据库资源
    rs.close();
    st.close();
    conn.close();
	}
}
```

# Tomcat

* 第一步:配置成功，能打开Apache Tomcat页面了
* 第二步:学习???（今天晚上看下）

# Java命名规范

1. 项目名全部小写

2. 包名全部小写

3. 类名首字母大写，如果类名由多个单词组成，每个单词的首字母都要大写。

   如：public class MyFirstClass{}

4. 变量名、方法名首字母小写，如果名称由多个单词组成，每个单词的首字母都要大写。

   如：int index=0;

   ​       public void toString(){}

5. 常量名全部大写

   如：public static final String GAME_COLOR=”RED”;

6. 所有命名规则必须遵循以下规则：

   1)名称只能由字母、数字、下划线、$符号组成

   2)不能以数字开头

   3)名称不能使用JAVA中的关键字。

   4)坚决不允许出现中文及拼音命名。
   
   (转至<https://www.cnblogs.com/zshibo/p/8007123.html>)