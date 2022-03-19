# 工厂方法模式

## Client.java

```
package com.bermuda.surface;

import com.bermuda.helper.OperationHelper;
import com.bermuda.util.AddFactory;
import com.bermuda.util.OperationFactory;

public class Client {
    public static void main(String[] args) {
        OperationFactory operationFactory = new AddFactory();
        OperationHelper operationHelper = operationFactory.getOperation();
        operationHelper.getResult(1,2);
    }
}
```

## OperationHelper.java

```
package com.bermuda.helper;

public abstract class OperationHelper {
    public abstract void getResult(int operationA,int operationB);
}
```

### OperationAdd.java

```
package com.bermuda.helper;

public class OperationAdd extends OperationHelper {
    @Override
    public void getResult(int operationA,int operationB) {
        System.out.println(operationA+operationB);
    }
}
```

### OperationSub.java

```
package com.bermuda.helper;

public class OperationSub extends OperationHelper {
    @Override
    public void getResult(int operationA, int operationB) {
        System.out.println(operationA-operationB);
    }
}
```

### OperationMul.java

```
package com.bermuda.helper;

public class OperationMul extends OperationHelper {
    @Override
    public void getResult(int operationA, int operationB) {
        System.out.println(operationA*operationB);
    }
}
```

### OperationDiv.java

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


## OperationFactory.java

```
package com.bermuda.util;

import com.bermuda.helper.*;

public abstract class OperationFactory {
    public abstract OperationHelper getOperation();
}
```

### AddFactory.java

```
package com.bermuda.util;

import com.bermuda.helper.OperationAdd;
import com.bermuda.helper.OperationHelper;

public class AddFactory extends OperationFactory {
    public OperationHelper getOperation() {
        return new OperationAdd();
    }
}
```

### SubFactory.java

```
package com.bermuda.util;

import com.bermuda.helper.OperationHelper;
import com.bermuda.helper.OperationSub;

public class SubFactory extends OperationFactory {
    public OperationHelper getOperation() {
        return new OperationSub();
    }
}
```

### MulFactory.java

```
package com.bermuda.util;

import com.bermuda.helper.OperationHelper;
import com.bermuda.helper.OperationMul;

public class MulFactory extends OperationFactory{
    public OperationHelper getOperation() {
        return new OperationMul();
    }
}
```

### DivFactory.java

```
package com.bermuda.util;

import com.bermuda.helper.OperationDiv;
import com.bermuda.helper.OperationHelper;

public class DivFactory extends OperationFactory {
    public OperationHelper getOperation() {
        return new OperationDiv();
    }
}
```