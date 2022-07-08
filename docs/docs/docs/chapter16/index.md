# 策略模式

## Client

```
package com.bermuda.surface;

import com.bermuda.context.OperationContext;

public class Client {
    public static void main(String[] args) {
        OperationContext operationContext = new OperationContext('+');
        operationContext.getResult(2,2);
    }
}
```

## OperationContext

```
package com.bermuda.context;

import com.bermuda.helper.*;

public class OperationContext {

    private OperationHelper operationHelper = null;

    /*
    消除switch看抽象工厂模式
     */
    public OperationContext(char operation) {
        switch (operation){
            case '+':
                operationHelper = new OperationAdd();
                break;
            case '-':
                operationHelper = new OperationSub();
                break;
            case '*':
                operationHelper = new OperationMul();
                break;
            case '/':
                operationHelper = new OperationDiv();
                break;
            default:
                operationHelper = null;
        }
    }

    public void getResult(int operationA,int operationB){
        operationHelper.getResult(operationA,operationB);
    }
}
```

## OperationHelper

```
package com.bermuda.helper;

public abstract class OperationHelper {
    public abstract void getResult(int operationA,int operationB);
}
```

### OperationAdd

```
package com.bermuda.helper;

public class OperationAdd extends OperationHelper {
    @Override
    public void getResult(int operationA,int operationB) {
        System.out.println(operationA+operationB);
    }
}
```

### OperationSub

```
package com.bermuda.helper;

public class OperationSub extends OperationHelper {
    @Override
    public void getResult(int operationA, int operationB) {
        System.out.println(operationA-operationB);
    }
}
```

### OperationMul

```
package com.bermuda.helper;

public class OperationMul extends OperationHelper {
    @Override
    public void getResult(int operationA, int operationB) {
        System.out.println(operationA*operationB);
    }
}
```

### OperationDiv

```
package com.bermuda.helper;

public class OperationDiv extends OperationHelper {
    @Override
    public void getResult(int operationA, int operationB) {
        if(operationB != 0){
            System.out.println(operationA/operationB);
        }else {
            System.out.println("除数不能为0");
        }
    }
}
```