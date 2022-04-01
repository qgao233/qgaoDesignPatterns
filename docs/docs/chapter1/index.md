# 中介者模式

## Client.java

```
package com.bermuda.surface;

import com.bermuda.background.ConcreteColleague1;
import com.bermuda.background.ConcreteColleague2;
import com.bermuda.background.ConcreteMediator;

public class Client {

    public static void main(String[] args) {
        ConcreteMediator mediator = new ConcreteMediator();

        ConcreteColleague1 concreteColleague1 = new ConcreteColleague1(mediator);
        ConcreteColleague2 concreteColleague2 = new ConcreteColleague2(mediator);

        mediator.setConcreteColleague1(concreteColleague1);
        mediator.setConcreteColleague2(concreteColleague2);

        concreteColleague1.send("how do you do");
        concreteColleague2.send("fine");
    }
}
```

## Colleague.java

```
package com.bermuda.background;

public abstract class Colleague {

    protected Mediator mediator;

    public Colleague(Mediator mediator) {
        this.mediator = mediator;
    }

    public abstract void send(String message);
    public abstract void notify(String message);
}
```

### ConcreteColleague1.java

```
package com.bermuda.background;

public class ConcreteColleague1 extends Colleague {
    public ConcreteColleague1(Mediator mediator) {
        super(mediator);
    }

    public void send(String message) {
        mediator.send(message,this);
    }

    public void notify(String message) {
        System.out.println("1 get "+message);
    }


}
```

### ConcreteColleague2.java

```
package com.bermuda.background;

public class ConcreteColleague2 extends Colleague {

    public ConcreteColleague2(Mediator mediator) {
        super(mediator);
    }

    public void send(String message) {
        mediator.send(message,this);
    }

    public void notify(String message) {
        System.out.println("2 get "+message);
    }
}
```

## Mediator.java

```
package com.bermuda.background;

public abstract class Mediator {
    public abstract void send(String message,Colleague colleague);
}
```

### ConcreteMediator.java

```
package com.bermuda.background;

public class ConcreteMediator extends Mediator{

    private ConcreteColleague1 concreteColleague1;
    private ConcreteColleague2 concreteColleague2;

    public void setConcreteColleague1(ConcreteColleague1 concreteColleague1) {
        this.concreteColleague1 = concreteColleague1;
    }

    public void setConcreteColleague2(ConcreteColleague2 concreteColleague2) {
        this.concreteColleague2 = concreteColleague2;
    }

    public void send(String message, Colleague colleague) {
        if(colleague == concreteColleague1){
            concreteColleague2.notify(message);
        }else {
            concreteColleague1.notify(message);
        }
    }
}
```