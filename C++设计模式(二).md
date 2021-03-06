
## 工厂模式

简单工厂，工厂方法，抽象工厂都属于设计模式中的创建型模式。其主要功能都是帮助我们把对象的实例化部分抽取了出来，优化了系统的架构，并且增强了系统的扩展性。

**简单工厂**

简单工厂模式的工厂类一般是使用静态方法，通过接收的参数的不同来返回不同的对象实例。

不修改代码的话，是无法扩展的。


![](https://github.com/MrFighting/CPP_GeekBand/blob/master/Date/SimpleFactory.jpg)


**工厂方法**

工厂方法是针对每一种产品提供一个工厂类。通过不同的工厂实例来创建不同的产品实例。

在同一等级结构中，支持增加任意产品。

![](https://github.com/MrFighting/CPP_GeekBand/blob/master/Date/FactoryMethod.jpg)

**抽象工厂**

抽象工厂是应对产品族概念的。比如说，每个汽车公司可能要同时生产轿车，货车，客车，那么每一个工厂都要有创建轿车，货车和客车的方法。

应对产品族概念而生，增加新的产品线很容易，但是无法增加新的产品。

![](https://github.com/MrFighting/CPP_GeekBand/blob/master/Date/AbstractFactory.jpg)

**小结**

★工厂模式中，重要的是工厂类，而不是产品类。产品类可以是多种形式，多层继承或者是单个类都是可以的。但要明确的，工厂模式的接口只会返回一种类型的实例，这是在设计产品类的时候需要注意的，最好是有父类或者共同实现的接口。

★使用工厂模式，返回的实例一定是工厂创建的，而不是从其他对象中获取的。

★工厂模式返回的实例可以不是新创建的，返回由工厂创建好的实例也是可以的。

 

**区别**

简单工厂 ： 用来生产同一等级结构中的任意产品。（对于增加新的产品，无能为力）

工厂方法 ：用来生产同一等级结构中的固定产品。（支持增加任意产品）   
抽象工厂 ：用来生产不同产品族的全部产品。（对于增加新的产品，无能为力；支持增加产品族）  

 

以上三种工厂 方法在等级结构和产品族这两个方向上的支持程度不同。所以要根据情况考虑应该使用哪种方法。

---

## 适配器模式

**适配器模式:** 根据原有的接口(adaptee),为了适配新的接口,引入一个中间类(adapter),
比如为了用dequeue的接口实现stack,就要在stack中适配dequeue的接口.

**例子:** 举一个生活中最常见的例子！就如我们的球类吧！如排球，如果只是想拿着排球在自行车老大爷那说点好的来打气是行不通，因为那的打气筒是无法往你的排球里灌入气体的，所以你得必备一个排球专用的气针才可啊！而在此“气针”则是“适配”。


![image](https://github.com/MrFighting/CPP_GeekBand/blob/master/Date/adapter.png)

> 模式所涉及的角色有：
> 
> 　　●　　目标(Target)角色：这就是所期待得到的接口。注意：由于这里讨论的是类适配器模式，因此目标不可以是类。
> 
> 　　●　　源(Adapee)角色：现在需要适配的接口。
> 
> 　　●　　适配器(Adaper)角色：适配器类是本模式的核心。适配器把源接口转换成目标接口。显然，这一角色不可以是接口，而必须是具体类。



```c++
class Target {

public:
    void sampleOperation1(); 
 
    void sampleOperation2(); 
}

class Adaptee {

public:
    void sampleOperation1(){}
    
}

class Adapter {
private:
    Adaptee* adaptee;
    
public: 
    Adapter(Adaptee* adaptee){
        this->adaptee = adaptee;
    }

public: 
    void sampleOperation1(){
        adaptee->sampleOperation1();
    }

    void sampleOperation2(){
        //写相关的代码
    }
}
```


---

## 代理模式

**代理模式的定义**：为其他对象提供一种代理以控制对这个对象的访问。在某些情况下，一个对象不适合或者不能直接引用另一个对象，而代理对象可以在客户端和目标对象之间起到中介的作用。


> **组成：**
> 
> 抽象角色：通过接口或抽象类声明真实角色实现的业务方法。
> 
> 代理角色：实现抽象角色，是真实角色的代理，通过真实角色的业务逻辑方法来实现抽象方法，并可以附加自己的操作。
> 
> 真实角色：实现抽象角色，定义真实角色所要实现的业务逻辑，供代理角色调用。

![](https://github.com/MrFighting/CPP_GeekBand/blob/master/Date/proxy.png)

> **什么时候使用代理模式**
> 
> 　　当我们需要使用的对象很复杂或者需要很长时间去构造，这时就可以使用代理模式(Proxy)。例如：如果构建一个对象很耗费时间和计算机资源，代理模式(Proxy)允许我们控制这种情况，直到我们需要使用实际的对象。一个代理(Proxy)通常包含和将要使用的对象同样的方法，一旦开始使用这个对象，这些方法将通过代理(Proxy)传递给实际的对象。 一些可以使用代理模式(Proxy)的情况：
> 
> 　　一个对象，比如一幅很大的图像，需要载入的时间很长。　　　　
> 
> 　　一个需要很长时间才可以完成的计算结果，并且需要在它计算过程中显示中间结果
> 
> 　　一个存在于远程计算机上的对象，需要通过网络载入这个远程对象则需要很长时间，特别是在网络传输高峰期。
> 
> 　　一个对象只有有限的访问权限，代理模式(Proxy)可以验证用户的权限
> 
> 　　代理模式(Proxy)也可以被用来区别一个对象实例的请求和实际的访问，例如：在程序初始化过程中可能建立多个对象，但并不都是马上使用，代理模式(Proxy)可以载入需要的真正的对象。这是一个需要载入和显示一幅很大的图像的程序，当程序启动时，就必须确定要显示的图像，但是实际的图像只能在完全载入后才可以显示！这时我们就可以使用代理模式(Proxy)。

**抽象对象角色**


```c++
class AbstractObject {
    //操作
public:
    vitual void operation() = 0;
}
```

**目标对象角色**


```c++
class RealObject : public AbstractObject {
public:
    void operation() {
        //一些操作
    }
}
```

```c++
class ObjProxy : public AbstractObject {
    RealObject* Robj;
public:
    ...//ctor
    void operation() {
        ...//operation before
        Robj->operation();
        ...//operation after
    }
}

```


**客户端**

```c++
int main() {
    RealObject* obj = new RealObject();
    AbstractObject* prox = new ObjProxy(obj);
    prox->operation();//执行代理动作
}

```

