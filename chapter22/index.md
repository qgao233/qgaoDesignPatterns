# 访问者模式

## Client

```
package com.bermuda.surface;

import com.bermuda.background.*;

public class Client {

    public static void main(String[] args) {
        ObjectStructure objectStructure = new ObjectStructure();

        objectStructure.attach(new Man());
        objectStructure.attach(new Woman());

        Success success = new Success();
        objectStructure.display(success);

        Marriage marriage = new Marriage();
        objectStructure.display(marriage);
    }
}
```

## ObjectStructure

```
package com.bermuda.background;

import java.util.ArrayList;
import java.util.List;

public class ObjectStructure {

    private List<Person> elements = new ArrayList<Person>();

    public void attach(Person element){
        elements.add(element);
    }

    public void detach(Person element){
        elements.remove(element);
    }

    public void display(Action visitor){
        for (Person e:elements
             ) {
            e.accept(visitor);
        }
    }
}
```

## Person

```
package com.bermuda.background;

public abstract class Person {
    public abstract void accept(Action visitor);
}
```

### Man

```
package com.bermuda.background;

public class Man extends Person {
    public void accept(Action visitor) {
        visitor.getManConclusion(this);
    }
}
```

### Woman

```
package com.bermuda.background;

public class Woman extends Person {
    public void accept(Action visitor) {
        visitor.getWomanConclusion(this);
    }
}
```

## Action

```
package com.bermuda.background;

public abstract class Action {
    public abstract void getManConclusion(Man concreteElementA);
    public abstract void getWomanConclusion(Woman concreteElementB);
}
```

### Success

```
package com.bermuda.background;

public class Success extends Action {
    public void getManConclusion(Man concreteElementA) {
        System.out.println(concreteElementA.getClass().getSimpleName()+" "+this.getClass().getSimpleName()+"时，背后多半有一个伟大的女人");
    }

    public void getWomanConclusion(Woman concreteElementB) {
        System.out.println(concreteElementB.getClass().getSimpleName()+" "+this.getClass().getSimpleName()+"时，背后大多有一个不成功的男人");
    }
}
```

### Marriage

```
package com.bermuda.background;

public class Marriage extends Action {
    public void getManConclusion(Man concreteElementA) {
        System.out.println(concreteElementA.getClass().getSimpleName()+" "+this.getClass().getSimpleName()+"时，感慨道：恋爱游戏终结时，‘有妻徒刑’遥无期");
    }

    public void getWomanConclusion(Woman concreteElementB) {
        System.out.println(concreteElementB.getClass().getSimpleName()+" "+this.getClass().getSimpleName()+"时，欣慰曰：爱情长跑路漫漫，婚姻保险保平安");
    }
}
```