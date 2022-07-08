# 原型模式(部分实现)

## Client.java

```
package com.bermuda.surface;

import com.bermuda.shallowCopy.Resume;

/**
 * prototype:原型模式
 */
public class Client {
    public static void main(String[] args) {
        //shallowCopy 这里出了点问题，不能复现浅复制，暂待解决
        Resume resume = new Resume();
        resume.setWorkExperience("2005");
        System.out.println(resume.getId()+"#"+resume.getWorkExperience().getWorkDate());

        Resume resume1 = (Resume)resume.clone();
        resume1.setWorkExperience("2008");
        System.out.println(resume.getId()+"#"+resume.getWorkExperience().getWorkDate());
        //
    }
}
```

## Resume.java

```
package com.bermuda.shallowCopy;

public class Resume implements Cloneable{
    private int id;
    private WorkExperience workExperience;

    public Resume() {
        this.id = 0;
        this.workExperience = new WorkExperience();
    }

    public int getId() {
        return id;
    }

    public void setId(int id) {
        this.id = id;
    }

    public WorkExperience getWorkExperience() {
        return workExperience;
    }

    public void setWorkExperience(String workDate) {
        this.workExperience.setWorkDate(workDate);
    }

    @Override
    public Object clone()  {
        Object object = null;
        try {
            object = super.clone();
        } catch (CloneNotSupportedException e) {
            e.printStackTrace();
        }
        return object;
    }
}
```

## WorkExperience.java

```
package com.bermuda.shallowCopy;

public class WorkExperience {
    private String workDate;

    public String getWorkDate() {
        return workDate;
    }

    public void setWorkDate(String workDate) {
        this.workDate = workDate;
    }
}
```