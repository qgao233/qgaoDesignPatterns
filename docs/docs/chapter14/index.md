# 模板方法模式

## Client

```
package com.bermuda.surface;

import com.bermuda.model.Answer;
import com.bermuda.model.Question;

public class Client {

    public static void main(String[] args) {
        Question zhang = new Answer();
        zhang.question1();
    }
}
```

## Question

```
package com.bermuda.model;

public abstract class Question {
    public void question1(){
        System.out.println("请问1+1=多少？A、1  B、2  C、3");
        System.out.println(answer1());
    }

    public abstract String answer1();
}
```

### Answer

```
package com.bermuda.model;

public class Answer extends Question {
    @Override
    public String answer1() {
        return "B";
    }
}
```