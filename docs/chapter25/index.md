# 对象池模式

## ResourcePool

```
public class ResourcePool {
    /* ResourcePool 资源池 */
    private Resource[] resources;
    private int index=0;
    
    public ResourcePool(){
        resources = new Resource[]{new Resource(),new Resource(),new Resource()};
    }

    public Resource getResource(){
        if(this.index == this.resources.length) return null;
        return resources[index++];
    };

    public boolean releaseResource(Resource resource){
        if(index == 0){
            return false;
        }else{
            this.resources[--index] = resource;
            return true;
        }
    }
}
```

## Resource

```
class Resource{
    /* Resource 资源 */
    private static long counter;
    private long id;
    {
        this.id = counter++;
    }
    public long get_id(){
        return this.id;
    }
}
```

## Client

```
class Client{
    /* Client 客户端 */
    public static void main(String[] args){
        ResourcePool pool = new ResourcePool();

        Resource resource1 = pool.getResource();
        Resource resource2 = pool.getResource();
        Resource resource3 = pool.getResource();

        System.out.println(resource1.get_id());
        System.out.println(resource2.get_id());
        System.out.println(resource3.get_id());

        pool.releaseResource(resource1);
        pool.releaseResource(resource2);
        pool.releaseResource(resource3);

        Resource resource4 = pool.getResource();
        System.out.println(resource4.get_id());
    }
}

/* Output:
    0
    1
    2
    2
*/
```