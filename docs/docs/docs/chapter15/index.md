# 状态模式

## Client

```
package com.bermuda.surface;

import com.bermuda.relativeClass.Work;

public class Client {

    public static void main(String[] args) {
        Work work = new Work();
        work.setHour(9);
        work.writeProgram();
        work.setHour(18);
        work.writeProgram();
    }
}
```

## Work

```
package com.bermuda.relativeClass;

public class Work {
    private State state;
    private double hour;
    private boolean finish;

    public Work() {
        this.state = new MorningState();
    }

    public void writeProgram(){
        state.writeProgram(this);
    }

    public State getState() {
        return state;
    }

    public void setState(State state) {
        this.state = state;
    }

    public double getHour() {
        return hour;
    }

    public void setHour(double hour) {
        this.hour = hour;
    }

    public boolean isFinish() {
        return finish;
    }

    public void setFinish(boolean finish) {
        this.finish = finish;
    }
}
```

## State

```
package com.bermuda.relativeClass;

public abstract class State {
    public abstract void writeProgram(Work work);
}
```

### MorningState

```
package com.bermuda.relativeClass;

public class MorningState extends State {

    public void writeProgram(Work work) {
        if(work.getHour() < 12){
            System.out.println(work.getHour()+"点:上午精神百倍");
        }else {
            work.setState(new NoonState());
            work.writeProgram();
        }
    }
}
```

### NoonState

```
package com.bermuda.relativeClass;

public class NoonState extends State {

    public void writeProgram(Work work) {
        if(work.getHour() < 13){
            System.out.println(work.getHour()+"点:中午该吃饭了");
        }else {
            work.setState(new AfternoonState());
            work.writeProgram();
        }
    }
}
```

### AfternoonState

```
package com.bermuda.relativeClass;

public class AfternoonState extends State {
    public void writeProgram(Work work) {
        if(work.getHour() < 17){
            System.out.println(work.getHour()+"点:下午恹恹一息");
        }else {
            System.out.println("该下班了");
        }
    }
}
```