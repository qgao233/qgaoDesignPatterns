# 享元模式

## Client.java

```
package com.bermuda.surface;

import com.bermuda.background.User;
import com.bermuda.background.Website;
import com.bermuda.background.WebsiteFactory;

public class Client {

    public static void main(String[] args) {
        WebsiteFactory websiteFactory = new WebsiteFactory();

        Website fx = websiteFactory.getWebsiteCatagory("product show");
        fx.use(new User("gao"));
    }
}
```

## Website.java

```
package com.bermuda.background;

public abstract class Website {

    public abstract void use(User user);
}
```

### ConcreteWebSite.java

```
package com.bermuda.background;

public class ConcreteWebSite extends Website {

    private String name;

    public ConcreteWebSite(String name) {
        this.name = name;
    }

    public void use(User user) {
        System.out.println("网站分类："+name+" 用户："+user.getName());
    }
}
```

## WebsiteFactory.java

```
package com.bermuda.background;

import java.util.Hashtable;

public class WebsiteFactory {

    private Hashtable<String,Website> flyweights = new Hashtable<String, Website>();

    public Website getWebsiteCatagory(String key){
        if(!flyweights.containsKey(key)){
            flyweights.put(key,new ConcreteWebSite(key));
        }
        return flyweights.get(key);
    }

    public int getWebSiteCount(){
        return flyweights.size();
    }
}
```

## User.java

```
package com.bermuda.background;

public class User {
    private String name;

    public User(String name) {
        this.name = name;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }
}
```