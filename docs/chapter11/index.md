# 建造者模式

## Client.java

```
package com.bermuda.surface;

import com.bermuda.builder.PersonFatBuilder;
import com.bermuda.director.PersonDirector;

public class Client {

    public static void main(String[] args) {
        new PersonDirector().construct(new PersonFatBuilder());
    }
}
```

## PersonDirector.java

```
package com.bermuda.director;

import com.bermuda.builder.PersonBuilder;

public class PersonDirector {

    public void construct(PersonBuilder personBuilder){
        personBuilder.buildHead();
        personBuilder.buildBody();
        personBuilder.buildLeftHand();
        personBuilder.buildRightHand();
        personBuilder.buildLeftFoot();
        personBuilder.buildRightFoot();
    }
}
```

## PersonBuilder.java

```
package com.bermuda.builder;

public abstract class PersonBuilder {

    public abstract void buildHead();
    public abstract void buildBody();
    public abstract void buildLeftHand();
    public abstract void buildRightHand();
    public abstract void buildLeftFoot();
    public abstract void buildRightFoot();
}
```

### PersonFatBuilder.java

```
package com.bermuda.builder;

public class PersonFatBuilder extends PersonBuilder {

    public void buildHead() {
        System.out.println("fat Head");
    }

    public void buildBody() {
        System.out.println("fat Body");
    }

    public void buildLeftHand() {
        System.out.println("fat LeftHand");
    }

    public void buildRightHand() {
        System.out.println("fat RightHand");
    }

    public void buildLeftFoot() {
        System.out.println("fat LeftFoot");
    }

    public void buildRightFoot() {
        System.out.println("fat RightFoot");
    }
}
```