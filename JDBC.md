# JDBC

<https://study.163.com/course/courseMain.htm?courseId=1005080015&_trace_c_p_k2_=1d815cb7de4a4875b9a967064ee0b71f>

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

