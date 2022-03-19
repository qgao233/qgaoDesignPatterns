# 抽象工厂模式

## Client.java

```
package com.bermuda.surface;

/**
 * 抽象工厂模式只是在工厂方法模式的基础上在factory接口中添加创建新对象的方法
 * 在本例中就是添加新的表，再在factory接口中添加对应的表对象的方法
 * 这里用简单工厂改造抽象工厂，再利用反射，使得程序由编译时转为运行时，
 * 即具体的对象生成可以利用properties文件通过反射获得
 */
public class Client {

    public static void main(String[] args) {

    }
}
```

## bean

```
package com.bermuda.bean;

public class User {
}
```

```
package com.bermuda.bean;

public class Department {
}
```

## dao

### DepartmentDao

```
package com.bermuda.dao;

import com.bermuda.bean.Department;

public interface DepartmentDao {

    public void insert(Department department);

    public void get(int id);
}
```

#### MysqlDepartmentDaoImpl

```
package com.bermuda.daoImpl;

import com.bermuda.bean.Department;
import com.bermuda.dao.DepartmentDao;

public class MysqlDepartmentDaoImpl implements DepartmentDao {
    public void insert(Department department) {
        System.out.println("mysql add department");
    }

    public void get(int id) {
        System.out.println("mysql get department");
    }
}
```

#### SqlServerDepartmentDaoImpl

```
package com.bermuda.daoImpl;

import com.bermuda.bean.Department;
import com.bermuda.dao.DepartmentDao;

public class SqlServerDepartmentDaoImpl implements DepartmentDao {
    public void insert(Department department) {
        System.out.println("sqlserver add department");
    }

    public void get(int id) {
        System.out.println("sqlserver get department");
    }
}
```

### UserDao

```
package com.bermuda.dao;

import com.bermuda.bean.User;

public interface UserDao {

    public void insert(User user);

    public void get(int id);
}
```



#### MysqlUserDaoImpl

```
package com.bermuda.daoImpl;

import com.bermuda.bean.User;
import com.bermuda.dao.UserDao;

public class MysqlUserDaoImpl implements UserDao{
    public void insert(User user) {
        System.out.println("mysql add user");
    }

    public void get(int id) {
        System.out.println("mysql get user");
    }
}
```

#### SqlServerUserDaoImpl

```
package com.bermuda.daoImpl;

import com.bermuda.bean.User;
import com.bermuda.dao.UserDao;

public class SqlServerUserDaoImpl implements UserDao {
    public void insert(User user) {
        System.out.println("sqlserver add user");
    }

    public void get(int id) {
        System.out.println("sqlserver get user");
    }
}
```

## dbFactory

### DataAccess

```
package com.bermuda.dbFactory;

import com.bermuda.dao.DepartmentDao;
import com.bermuda.dao.UserDao;
import com.bermuda.daoImpl.MysqlDepartmentDaoImpl;
import com.bermuda.daoImpl.MysqlUserDaoImpl;

public class DataAccess {

    private static String database = "Mysql";
//    private static String database = "SqlServer";

    public static UserDao createUserDao(){
        //这里根据反射和database字符串获得相应对象实例
        return new MysqlUserDaoImpl();
    }

    public static DepartmentDao createDepartmentDao(){
        //这里根据反射和database字符串获得相应对象实例
        return new MysqlDepartmentDaoImpl();
    }
}
```