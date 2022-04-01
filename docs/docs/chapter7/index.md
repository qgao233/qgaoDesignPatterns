# 备忘录模式

## Client.java

```
package com.bermuda.surface;

import com.bermuda.relativeClass.Caretaker;
import com.bermuda.relativeClass.GameRole;
import com.bermuda.relativeClass.Memento;

/**
 * 主要就是对内部实现进行封装
 */
public class Client {

    public static void main(String[] args) {
        GameRole zhang = new GameRole();
        Caretaker caretaker = new Caretaker();
        caretaker.setMemento(zhang.saveState());

        zhang.fight();

        zhang.recoverState(caretaker.getMemento());
    }
}
```

## Caretaker.java

```
package com.bermuda.relativeClass;

public class Caretaker {
    private Memento memento;

    public Memento getMemento() {
        return memento;
    }

    public void setMemento(Memento memento) {
        this.memento = memento;
    }
}
```

## GameRole.java

```
package com.bermuda.relativeClass;

public class GameRole {

    private int attack;
    private int defend;

    public GameRole() {
        this.attack = 100;
        this.defend = 100;
    }

    public void fight(){
        this.attack -= 50;
        this.defend -= 50;
        System.out.println("战斗力降低了");
    }

    public Memento saveState(){
        System.out.println("保存进度");
        return new Memento(attack,defend);
    }

    public void recoverState(Memento memento){
        this.attack = memento.getAttack();
        this.defend = memento.getDefend();
        System.out.println("恢复进度");
    }
}
```

## Memento.java

```
package com.bermuda.relativeClass;

public class Memento {

    private int attack;
    private int defend;

    public Memento(int attack, int defend) {
        this.attack = attack;
        this.defend = defend;
    }

    public int getAttack() {
        return attack;
    }

    public void setAttack(int attack) {
        this.attack = attack;
    }

    public int getDefend() {
        return defend;
    }

    public void setDefend(int defend) {
        this.defend = defend;
    }
}
```