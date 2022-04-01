# 单例模式-多线程

## 饿汉单例

```
package com.bermuda.relativeClass;


/**
 * 饿汉单例
 */
public class HungrySingleton {

    private static final HungrySingleton instance = new HungrySingleton();

    private HungrySingleton(){

    }

    public static HungrySingleton getInstance() {
        return instance;
    }
}
```

## 懒汉单例

```
package com.bermuda.relativeClass;


/**
 * 懒汉单例
 */
public class LazySingleton {

    private static volatile LazySingleton instance;
    private static Object object = new Object();

    private LazySingleton(){

    }

    public static LazySingleton getInstance() {
        if(instance == null){
            synchronized (object){
                if(instance == null){
                    instance = new LazySingleton();
                }
            }
        }
        return instance;
    }
}
```