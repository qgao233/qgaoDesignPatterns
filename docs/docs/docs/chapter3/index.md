# 代理模式

## Client.java

```
package com.bermuda.surface;

import com.bermuda.entityImpl.Proxy;

public class Client {

    public static void main(String[] args) {
        Proxy proxy = new Proxy("lianlian");
        proxy.giveFlower();
        proxy.giveMoney();
    }
}
```

## GivenGift.java

```
package com.bermuda.entity;

public interface GivenGift {

    void giveFlower();
    void giveMoney();
}
```

### RealMan.java

```
package com.bermuda.entityImpl;

import com.bermuda.entity.GivenGift;

public class RealMan implements GivenGift {

    private String name;

    public RealMan(String name) {
        this.name = name;
    }

    public void giveFlower() {
        System.out.println("送"+name+"花");
    }

    public void giveMoney() {
        System.out.println("送"+name+"钱");
    }
}
```

### Proxy.java

```
package com.bermuda.entityImpl;

import com.bermuda.entity.GivenGift;

public class Proxy implements GivenGift {

    RealMan realMan = null;

    public Proxy(String name) {
        this.realMan = new RealMan(name);
    }

    public void giveFlower() {
        realMan.giveFlower();
    }

    public void giveMoney() {
        realMan.giveMoney();
    }
}
```