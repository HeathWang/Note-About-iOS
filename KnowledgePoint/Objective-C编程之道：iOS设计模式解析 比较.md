# Objective-C编程之道：iOS设计模式解析 比较

## 多态

OC中的多态：
1. 通过子类继承父类表现多态。子类自动继承了父类的方法，同时子类可以复写 `override` 父类方法，这样**同一种行为**（这里指方法）有了不同的表现。
2. 依托协议 `protocol` 。不同的对象实现同一种协议，那么这些对象同时具备了某些方法，但不同对象对协议的实现可能是不同的。调用者不用关心具体实现，只需要调用对象该方法即可。


## 使用中介者（Mediator）协调视图


> 中介者模式是指用一个对象来封装一组对象之间的交互逻辑。中介者通过避免对象间显式的相互引用来增进不同对象间的松耦合(Loose coupling)。因此对象间的交互可以集中在一处控制，对象间的依存关系将减少。

![Screenshot 2018-12-03 11.32.25](media/15438072164605/Screenshot%202018-12-03%2011.32.25.png)

### 思考

在现有的流行组件化设计中，组件之间的相互通信有一下几种方式：
1. url注册
2. protocol协议
3. target-action

target-action中，依托中介者Mediator来实现Controller之间的跳转。


## 抽象工厂和工厂方法

### 相同点

创建对象而不让客户端知晓返回了什么确切的具体对象。

### 不同点

1. 抽象工厂通过对象组合创建抽象产品，而工厂方法通过类继承创建抽象产品。
2. 抽象工厂创建多系列产品，工厂方法创建一种产品
3. 抽象工厂必须修改父类的接口才能支持新的产品，而工厂方法通过子类化创建者并重载工厂方法以创建新产品。

引申到Cocoa中：
类簇是抽象工厂的一种形式，比如NSNumber本身是一个高度抽象的工厂，而`NSCFBoolean`和`NSCFNumber`是具体工厂子类。子类是具体工厂，因为他们重载了NSNumber中声明的公有工厂方法以生产产品。例如，`intValue`和`boolValue`根据实际NSNumber对象的内部返回一个值。

类似的还有NSarray。


## 生成器

一般用在复杂的初始化对象中。有一个builder对象去初始化。


## 单例

Cocoa Touch中的单例：
UIApplication，NSFileManager，NSUserDefault

## 适配器模式

* delegate代理
* Block

## 外观模式

什么时候考虑使用？
* 子系统正在逐渐变得复杂，应用模式的过程中会演化出许多类。可以使用外观模式为这些子系统类提供一个较简单的接口。
* 可以使用外观对子系统进行分层。每个子系统级别有一个外观作为入口，让它们通过外观进行通信，可以简化依赖关系。

一个常见的列子：乘客乘坐出租车，告诉司机‘送我到xx地方’。司机开始执行一系列命令，驾驶汽车，最终送到目的地。

![Screenshot 2018-12-07 11.36.22](media/15438072164605/Screenshot%202018-12-07%2011.36.22.png)


## 观察者模式

观察者模式也叫发布-订阅模式。一对多关系，发布者对多个订阅者。

Cocoa Touch框架中用2种技术改写了观察者模式：`通知`和`KVO`。


## 组合模式

在Cocoa Touch中，UIView被组织成一个组合结构。每个UIView的实例可以包含UIView的其他实例，形成统一的树状结构。

组合模式的主要意图是让树状结构中的每个节点具有相同的抽象接口。
组合结构的内部不应该暴露给客户端，因此组合模式总是跟**迭代器模式**一起使用。

想一想UIView的遍历？


## 访问者模式

## 装饰模式

使用category来装饰类。形象的说，现在有一张照片（类同**类**），我们可以给相片放到不同的相框（类同**category**）来装饰它。


## 模板方法

模板方法主要是最顶级父类定义抽象方法，但是不实现，具体的实现交给子类。

在RAC中`RACStream`是其他RACSignal，RACSubject等类的超类，就使用了这种模式。同时为了保证子类必须自己实现模板方法，需要在超类中抛出异常：


```Objective-C
+ (__kindof RACStream *)empty {
	NSString *reason = [NSString stringWithFormat:@"%@ must be overridden by subclasses", NSStringFromSelector(_cmd)];
	@throw [NSException exceptionWithName:NSInternalInconsistencyException reason:reason userInfo:nil];
}
```

### Cocoa Touch中的模板方法


```
- (void)drawRect:(CGRect)rect;
```

> The default implementation of this method **does nothing**. Subclasses that use technologies such as Core Graphics and UIKit to draw their view’s content should override this method and implement their drawing code there. You do not need to override this method if your view sets its content in other ways. For example, you do not need to override this method if your view just displays a background color or if your view sets its content directly using the underlying layer object.


## 备忘录

iOS中的NSCoder进行编码和解码就用到了备忘录模式。

