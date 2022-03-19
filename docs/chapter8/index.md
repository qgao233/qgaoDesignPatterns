# 外观模式-门面模式

## Client.java

```
package com.bermuda.surface;

import com.bermuda.Manage.Fund;

public class Client {

    public static void main(String[] args) {
        Fund fund = new Fund();
        fund.buy();
        fund.sell();
    }
}
```

## Fund.java

```
package com.bermuda.Manage;

import com.bermuda.duty.NationalDebt;
import com.bermuda.duty.Realty;
import com.bermuda.duty.Stock;

/**
 * 门面
 */
public class Fund {
    private Stock stock;
    private Realty realty;
    private NationalDebt nationalDebt;

    public Fund() {
        this.stock = new Stock();
        this.realty = new Realty();
        this.nationalDebt = new NationalDebt();
    }

    public void buy(){
        stock.buy();
        realty.buy();
        nationalDebt.buy();
    }

    public void sell(){
        stock.sell();
        realty.sell();
        nationalDebt.sell();
    }
}
```

## NationalDebt.java

```
package com.bermuda.duty;

/**
 * 国债
 */
public class NationalDebt {

    public void buy(){
        System.out.println("buy NationalDebt");
    }

    public void sell(){
        System.out.println("sell NationalDebt");
    }
}
```

## Realty.java

```
package com.bermuda.duty;

/**
 * 房地产
 */
public class Realty {

    public void buy(){
        System.out.println("buy Realty");
    }

    public void sell(){
        System.out.println("sell Realty");
    }
}
```

## Stock.java

```
package com.bermuda.duty;

/**
 * 股份
 */
public class Stock {

    public void buy(){
        System.out.println("buy stock");
    }

    public void sell(){
        System.out.println("sell stock");
    }
}
```