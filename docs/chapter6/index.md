# 命令模式

## Client.java

```
package com.bermuda.surface;

import com.bermuda.related.Command;
import com.bermuda.related.ConcreteCommand;
import com.bermuda.related.Invoker;
import com.bermuda.related.Receiver;

public class Client {

    public static void main(String[] args) {
        Receiver receiver = new Receiver();
        Command command = new ConcreteCommand(receiver);
        Invoker invoker = new Invoker();

        invoker.setCommand(command);
        invoker.executeCommand();
    }
}
```

## Command.java

```
package com.bermuda.related;

public abstract class Command {

    protected Receiver receiver;

    public Command(Receiver receiver) {
        this.receiver = receiver;
    }

    public abstract void execute();
}
```

### ConcreteCommand.java

```
package com.bermuda.related;

public class ConcreteCommand  extends Command{

    public ConcreteCommand(Receiver receiver) {
        super(receiver);
    }

    public void execute() {
        receiver.action();
    }
}
```

## Invoker.java

```
package com.bermuda.related;

public class Invoker {

    private Command command;

    public void setCommand(Command command) {
        this.command = command;
    }

    public void executeCommand(){
        command.execute();
    }
}
```

## Receiver.java

```
package com.bermuda.related;

public class Receiver {

    public void action(){
        System.out.println("执行请求");
    }
}
```