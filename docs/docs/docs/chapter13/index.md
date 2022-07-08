# 桥接模式

## Client

```
package com.bermuda.surface;

import com.bermuda.brand.OnePlusPhoneBrand;
import com.bermuda.brand.PhoneBrand;
import com.bermuda.soft.GameSoft;

public class Client {

    public static void main(String[] args) {
        PhoneBrand phoneBrand = new OnePlusPhoneBrand("一加",new GameSoft());
        phoneBrand.run();
    }
}
```

## PhoneBrand

```
package com.bermuda.brand;

import com.bermuda.soft.PhoneSoft;

public abstract class PhoneBrand {

    protected String name;
    protected PhoneSoft phoneSoft;

    public PhoneBrand(String name, PhoneSoft phoneSoft) {
        this.name = name;
        this.phoneSoft = phoneSoft;
    }

    public abstract void run();
}
```

### OnePlusPhoneBrand

```
package com.bermuda.brand;

import com.bermuda.soft.PhoneSoft;

public class OnePlusPhoneBrand extends PhoneBrand {

    public OnePlusPhoneBrand(String name, PhoneSoft phoneSoft) {
        super(name, phoneSoft);
    }

    public void run() {
        System.out.println(name+":"+phoneSoft.run());
    }
}
```



### XiaomiPhoneBrand

```
package com.bermuda.brand;

import com.bermuda.soft.PhoneSoft;

public class XiaomiPhoneBrand extends PhoneBrand {

    public XiaomiPhoneBrand(String name, PhoneSoft phoneSoft) {
        super(name, phoneSoft);
    }

    public void run() {
        System.out.println(name+":"+phoneSoft.run());
    }
}
```

## PhoneSoft

```
package com.bermuda.soft;

public abstract class PhoneSoft {
    public abstract String run();
}
```

### GameSoft

```
package com.bermuda.soft;

public class GameSoft extends PhoneSoft {
    public String run() {
        return "run game";
    }
}
```

### Mp3Soft

```
package com.bermuda.soft;

public class Mp3Soft extends PhoneSoft {
    public String run() {
        return "run mp3";
    }
}
```

