## 代码

### 设计模式

#### 单例模式

例模式分三种：懒汉式单例、饿汉式单例、登记式单例三种。
单例模式有如下特点：
-　1、单例类只能有一个实例。
-　2、单例类必须自己自己创建自己的唯一实例。
-　3、单例类必须给所有其他对象提供这一实例。

```java
public class Singleton {
    private static Singleton uniqueInstance = null;
    private Singleton() {
       // Exists only to defeat instantiation.
    }
    public static Singleton getInstance() {
       if (uniqueInstance == null) {
           uniqueInstance = new Singleton();
       }
       return uniqueInstance;
    }
    // Other methods...
}
```
三类，饿汉式，懒汉式，登记式
---

```java
//饿汉式单例类.在类初始化时，已经自行实例化 
 public class Singleton1 {
     //私有的默认构造子
     private Singleton1() {}
     //已经自行实例化 
     private static final Singleton1 single = new Singleton1();
     //静态工厂方法 
     public static Singleton1 getInstance() {
         return single;
     }
 }
 ```java
 import java.util.HashMap;
 import java.util.Map;
 //登记式单例类.
 //类似Spring里面的方法，将类名注册，下次从里面直接获取。
 public class Singleton3 {
     private static Map<String,Singleton3> map = new HashMap<String,Singleton3>();
     static{
         Singleton3 single = new Singleton3();
         map.put(single.getClass().getName(), single);
     }
     //保护的默认构造子
     protected Singleton3(){}
     //静态工厂方法,返还此类惟一的实例
     public static Singleton3 getInstance(String name) {
         if(name == null) {
             name = Singleton3.class.getName();
             System.out.println("name == null"+"--->name="+name);
         }
         if(map.get(name) == null) {
             try {
                 map.put(name, (Singleton3) Class.forName(name).newInstance());
             } catch (InstantiationException e) {
                 e.printStackTrace();
             } catch (IllegalAccessException e) {
                 e.printStackTrace();
             } catch (ClassNotFoundException e) {
                 e.printStackTrace();
             }
         }
         return map.get(name);
     }
     //一个示意性的商业方法
     public String about() {    
         return "Hello, I am RegSingleton.";    
     }    
     public static void main(String[] args) {
         Singleton3 single3 = Singleton3.getInstance(null);
         System.out.println(single3.about());
     }
 }
 ```
 ```java
 //懒汉式单例类.在第一次调用的时候实例化 
 public class Singleton2 {
     //私有的默认构造子
     private Singleton2() {}
     //注意，这里没有final    
     private static Singleton2 single=null;
     //静态工厂方法 
     public synchronized  static Singleton2 getInstance() {
          if (single == null) {  
              single = new Singleton2();
          }  
         return single;
     }
 }
 ```
