# 委托模式

## Client.java

```
package com.bermuda.surface;

import com.bermuda.informer.Boss;
import com.bermuda.informer.Informer;
import com.bermuda.observer.Observer;
import com.bermuda.observer.StockObserver;

/**
 * 先有了观察者模式，再有的委托模式（弥补了观察者模式的不足）
 */
public class Client {

    public static void main(String[] args) {
        Informer boss = new Boss();

        StockObserver stockObserver1 = new StockObserver(boss,"stockObserver1");
        StockObserver stockObserver2 = new StockObserver(boss,"stockObserver2");

        boss.attach("stockObserver1",stockObserver1,"closeStock");
        boss.attach("stockObserver2",stockObserver2,"closeStock");

        boss.setInformerState("boss come in");
        boss.notice();
    }
}
```

## Informer.java

```
package com.bermuda.informer;

import com.bermuda.handler.EventHandler;
import com.bermuda.observer.Observer;

public abstract class Informer {

    private String informerState;
    protected EventHandler eventHandler = new EventHandler();

    public String getInformerState() {
        return informerState;
    }

    public void setInformerState(String informerState) {
        this.informerState = informerState;
    }

    public abstract void attach(String description,Object object, String methodName, Object...params);
    public abstract void detach(String description);

    public abstract void notice();
}
```

### Boss.java

```
package com.bermuda.informer;

import com.bermuda.observer.Observer;

import java.util.ArrayList;
import java.util.List;

public class Boss extends Informer {

    public void attach(String description,Object object, String methodName, Object...params) {
        eventHandler.addEvent(description,object,methodName,params);
    }

    public void detach(String description) {
        eventHandler.removeEvent(description);
    }

    public void notice() {
        try {
            eventHandler.notifyAllEvents();
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```

## EventHandler.java

```
package com.bermuda.handler;

import java.util.ArrayList;
import java.util.HashMap;
import java.util.List;
import java.util.Map;

public class EventHandler {

    private Map<String,Event> eventMap = new HashMap<String, Event>();

    public void addEvent(String description,Object object, String methodName, Object...params){
        eventMap.put(description,new Event(object,methodName,params));
    }

    public void removeEvent(String description){
        if(eventMap.containsKey(description)){
            eventMap.remove(description);
        }else {
            System.out.println("no this event");
        }

    }

    public void notifyAllEvents() throws Exception{
        for(Event event:eventMap.values()){
            event.invoke();
        }
    }
}
```

## Event.java

```
package com.bermuda.handler;

import java.lang.reflect.Method;

public class Event {

    //要执行方法的对象
    private Object object;
    //要执行的方法名称
    private String methodName;
    //要执行方法的参数
    private Object[] params;
    //要执行方法的参数类型
    private Class[] paramTypes;

    public Event() {
    }

    public Event(Object object, String methodName, Object...params) {
        this.object = object;
        this.methodName = methodName;
        this.params = params;
        contractParamTypes(params);
    }

    //根据参数数组生成参数类型数组
    private void contractParamTypes(Object[] params){
        this.paramTypes=new Class[params.length];
        for(int i=0;i<params.length;i++){
            this.paramTypes[i]=params[i].getClass();
        }
    }

    public void invoke() throws Exception{
        Method method=object.getClass().getMethod(methodName,paramTypes);
        if(null==method){
            return;
        }
        method.invoke(object, params);
    }
}
```



## Observer.java

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

}
```

## StockObserver.java

```
package com.bermuda.observer;

import com.bermuda.informer.Informer;

public class StockObserver {

    private Informer informer;
    private String observerName;

    public StockObserver(Informer informer, String observerName) {
        this.informer = informer;
        this.observerName = observerName;
    }

    public void closeStock() {
        System.out.println(informer.getInformerState()+":"+observerName+" close the stock situation");
    }
}
```