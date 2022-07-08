# 适配器模式-对象

## Client

```
package com.bermuda.surface;

import com.bermuda.relativeClass.Adapter;
import com.bermuda.relativeClass.Target;

public class Client {

    public static void main(String[] args) {
        Target target = new Adapter();
        target.request();
    }
}
```

## Target

```
package com.bermuda.relativeClass;

public class Target {
    public void request(){
        System.out.println("普通请求");
    }
}
```

### Adapter

```
package com.bermuda.relativeClass;

public class Adapter extends Target {

    private Adaptee adaptee = new Adaptee();
    @Override
    public void request() {
        adaptee.specificRequest();
    }
}
```

## Adaptee

```
package com.bermuda.relativeClass;

public class Adaptee {
    public void specificRequest(){
        System.out.println("特殊请求");
    }
}
```