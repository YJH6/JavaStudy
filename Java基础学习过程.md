# Java学习过程

## [1]学习Java语言基础

下载Java核心技术卷一.pdf

<http://www.java1234.com/a/javabook/javabase/2018/0413/10949.html>

- Java常规代码

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

- 就我们现学的C++来说，Java的循环没怎么变

```java
for (int element : a) 
	{	
    	System.out.println(element)//这个就是打印a中所有元素了
	}//a必须为数组或者一个实现了 Iterable 接口的类对象？？
```

- break使用的不同

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

- 数组的不同

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

