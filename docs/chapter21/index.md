# 观察者模式

## Client

```
package com.bermuda.surface;

import com.bermuda.informer.Boss;
import com.bermuda.informer.Informer;
import com.bermuda.observer.Observer;
import com.bermuda.observer.StockObserver;

public class Client {

    public static void main(String[] args) {
        Informer boss = new Boss();

        Observer stockObserver1 = new StockObserver(boss,"stockObserver1");
        Observer stockObserver2 = new StockObserver(boss,"stockObserver2");

        boss.attach(stockObserver1);
        boss.attach(stockObserver2);

        boss.setInformerState("boss come in");
        boss.notice();
    }
}
```

## Informer

```
package com.bermuda.informer;

import com.bermuda.observer.Observer;

public abstract class Informer {

    private String informerState;

    public String getInformerState() {
        return informerState;
    }

    public void setInformerState(String informerState) {
        this.informerState = informerState;
    }

    public abstract void attach(Observer observer);
    public abstract void detach(Observer observer);

    public abstract void notice();
}
```

### Boss

```
package com.bermuda.informer;

import com.bermuda.observer.Observer;

import java.util.ArrayList;
import java.util.List;

public class Boss extends Informer {

    private List<Observer> observerList = new ArrayList<Observer>();

    public void attach(Observer observer) {
        observerList.add(observer);
    }

    public void detach(Observer observer) {
        observerList.remove(observer);
    }

    public void notice() {
        for (Observer observer:observerList) {
            observer.doAction();
        }
    }
}
```

## Observer

```
package com.bermuda.observer;

import com.bermuda.informer.Informer;

public abstract class Observer {
    protected Informer informer;
    protected String observerName;

    public Observer(Informer informer, String observerName) {
        this.informer = informer;
        this.observerName = observerName;
    }

    public abstract void doAction();
}
```

### StockObserver

```
package com.bermuda.observer;

import com.bermuda.informer.Informer;

public class StockObserver extends Observer {

    public StockObserver(Informer informer, String observerName) {
        super(informer, observerName);
    }

    public void doAction() {
        System.out.println(informer.getInformerState()+":"+observerName+"close the stock situation");
    }
}
```