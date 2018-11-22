# iOS中各种架构理解

# MVC （Model-View-Controller）
## 在扩展中进行代码重用
要在不同的 view controller 间共享代码，一个常见的方法是创建一个包含共通功能的父类。然后 view controller 就可以通过子类来获得这些功能了。这种技术可以工作，但是它有一个潜在的不足：我们只能为我们的新类选定单个父类。比如说，我们不能同时继承 UIPageViewController 和 UITableViewController。这种方式还经常会导致我们常说的**上帝 view controller** 的问题：一个共享的父类包括了项目中全部的共享的功能。这样的类通常会变得非常复杂，难以维护。

在 view controller 中共享代码的另一种选择是使用扩展。在多个 view controller 中都出现的方法有时候能够被添加到 UIViewController 的扩展中去。这样一来，所有的 view controller 就都能获取这个方法了。比如，我们可以为 UIViewController 添加一个显示文本警告的简便方法。

## 利用 Child View Controller 进行代码重用
将部分功能拆分到子viewController中

## 提取对象
比如UITableView的dataSource，我们可以提取到特定的对象里去。

## 简化View配置代码
通常来说，我们在ViewController中有太多的对view初始化以及配置的操作。
例如对于tableView的cellforRowAtIndexPath中，对cell的配置工作，是可以移到相关的cell中的，这样简化了Controller。

# MVVM (Model-View-View-Model)
![Screenshot 2018-11-21 14.16.46](media/15404515382837/Screenshot%202018-11-21%2014.16.46.png)

MVVM把以前ViewController做的工作转移到了View-Model中，通过数据绑定来关联View和Model。





