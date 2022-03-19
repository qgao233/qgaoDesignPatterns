# 简单工厂模式

## Client

```
package com.bermuda.surface;

import com.bermuda.helper.OperationHelper;
import com.bermuda.util.OperationFactory;

public class Client {
    public static void main(String[] args) {
        OperationHelper operationHelper = OperationFactory.getOperation('+');
        operationHelper.getResult(1,2);
    }
}
```

## OperationFactory

```
package com.bermuda.util;

import com.bermuda.helper.*;

public class OperationFactory {
    public static OperationHelper getOperation(char operation){
        OperationHelper operationHelper = null;
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
        return operationHelper;
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