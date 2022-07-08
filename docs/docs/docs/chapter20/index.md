# 装饰模式

## Client

```
package com.bermda.surface;

import com.bermda.entity.People;
import com.bermda.entityImpl.PeopleImpl;
import com.bermda.entityImpl.Skirts;
import com.bermda.entityImpl.Socks;

public class Client {
    public static void main(String[] args) {
        People people = new PeopleImpl("zhang");
        Skirts skirts = new Skirts();
        Socks socks = new Socks();

        skirts.setPeople(people);
        socks.setPeople(skirts);
        socks.action();
    }
}
```

## People

```
package com.bermda.entity;

public abstract class People {
    public abstract void action();
}
```

### PeopleImpl

```
package com.bermda.entityImpl;

import com.bermda.entity.People;

public class PeopleImpl extends People {

    private String name;

    public PeopleImpl(String name) {
        this.name = name;
    }

    @Override
    public void action() {
        System.out.println(name+" equiped:");
    }
}
```

### Clothes

```
package com.bermda.entity;

public class Clothes extends People{

    private People people = null;

    public void setPeople(People people) {
        this.people = people;
    }

    @Override
    public void action() {
        if(people != null){
            people.action();
        }
    }
}
```

#### Skirts

```
package com.bermda.entityImpl;

import com.bermda.entity.Clothes;

public class Skirts extends Clothes {
    @Override
    public void action() {
        super.action();
        System.out.print("skirts ");
    }
}
```

#### Socks

```
package com.bermda.entityImpl;

import com.bermda.entity.Clothes;

public class Socks extends Clothes {
    @Override
    public void action() {
        super.action();
        System.out.print("socks ");
    }
}
```

#### Tshirt

```
package com.bermda.entityImpl;

import com.bermda.entity.Clothes;

public class Tshirt extends Clothes {
    @Override
    public void action() {
        super.action();
        System.out.print("T-shirt ");
    }
}
```