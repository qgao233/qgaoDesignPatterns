# 职责链模式

## Client

```
package com.bermuda.surface;

import com.bermuda.Background.CommonManager;
import com.bermuda.Background.GeneralManager;
import com.bermuda.Background.MajorManager;
import com.bermuda.Background.Request;

public class Client {

    public static void main(String[] args) {
        CommonManager a = new CommonManager("a");
        MajorManager b = new MajorManager("b");
        GeneralManager c = new GeneralManager("c");

        a.setSuperior(b);
        b.setSuperior(c);

        Request request = new Request();
        request.setRequestType("请假");
        request.setNumber(3);

        a.requestApplication(request);
    }
}
```

## Manager

```
package com.bermuda.Background;

public abstract class Manager {
    protected String name;
    protected Manager superior;

    public Manager(String name) {
        this.name = name;
    }

    public void setSuperior(Manager superior) {
        this.superior = superior;
    }

    public abstract void requestApplication(Request request);
}
```

### CommonManager

```
package com.bermuda.Background;

public class CommonManager extends Manager {


    public CommonManager(String name) {
        super(name);
    }

    public void requestApplication(Request request) {
        if(request.getRequestType().equals("请假") && request.getNumber() <= 2){
            System.out.println(name+"允许"+request.getRequestType()+request.getNumber()+"天");
        }else {
            if(superior != null){
                superior.requestApplication(request);
            }
        }
    }
}
```

### GeneralManager

```
package com.bermuda.Background;

public class GeneralManager extends Manager {

    public GeneralManager(String name) {
        super(name);
    }

    public void requestApplication(Request request) {
        if(request.getRequestType().equals("请假")){
            System.out.println(name+"允许"+request.getRequestType()+request.getNumber()+"天");
        }else if (request.getRequestType().equals("加薪") && request.getNumber() <= 500){
            System.out.println(name+"允许"+request.getRequestType()+request.getNumber()+"天");
        }else {
            System.out.println("没有此请求对应的处理者");
        }
    }
}
```

### MajorManager

```
package com.bermuda.Background;

public class MajorManager extends Manager {

    public MajorManager(String name) {
        super(name);
    }

    public void requestApplication(Request request) {
        if(request.getRequestType().equals("请假") && request.getNumber() <= 5){
            System.out.println(name+"允许"+request.getRequestType()+request.getNumber()+"天");
        }else {
            if(superior != null){
                superior.requestApplication(request);
            }
        }
    }
}
```

## Request

```
package com.bermuda.Background;

public class Request {

    private String requestType;
    private String requestContent;
    private int number;

    public String getRequestType() {
        return requestType;
    }

    public void setRequestType(String requestType) {
        this.requestType = requestType;
    }

    public String getRequestContent() {
        return requestContent;
    }

    public void setRequestContent(String requestContent) {
        this.requestContent = requestContent;
    }

    public int getNumber() {
        return number;
    }

    public void setNumber(int number) {
        this.number = number;
    }
}
```