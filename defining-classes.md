#定义类 - Defining Classes 
当你为 OS X 或 iOS 系统编写软件时，你的大部分时间都花在了对象上。objective - c中的对象就像其他面向对象编程语言中的对象一样:它们把数据与相关的行为打包。  

一个应用程序构成了一个巨大的联通对象的生态系统，他们之间相互通信以解决具体问题，如显示一个可视化界面,响应用户的输入,或存储信息。 OS X 或 iOS 开发中,您不需要从头开始创建对象来解决每个问题； Cocoa (for OS X) 和 Cocoa Touch (for iOS) 为你提供一个包含可供你使用的现有对象库。 

其中一些对象是立即可用的,比如字符串和数字等基本数据类型,或像按钮和表视图这样的用户界面元素。一些是专为你以你需要的方式定制代码。软件开发过程涉及决定如何最好地定制和合并底层框架提供的对象和自己的对象,让你的应用具有其独特的特性和功能。  

在面向对象的编程术语中,对象类的实例。本章示范了如何在 objective – c 中通过声明一个用来描述你打算使用的类及其实例的接口来定义类。这个接口包含此类可以接收到的消息列表,所以你还需要提供类的实现,其中包含要执行的代码以响应每个消息。  

##类是对象的蓝图 - Classes Are Blueprints for Objects 
类描述了特定类型的对象的常见行为和属性。字符串对象(在 objective – c 中,这是类 NSString 的一个实例),该类提供了各种方法来检查和转换内部的字符。同样,此类过去常用于描述一个数字对象( NSNumber )提供围绕内部的数值,如将该值转换为不同数字类型的功能。 

同样的,多个由相同的蓝图构成的建筑在结构上是相同的,类的每个实例共享相同的属性和行为来作为该类的所有其他实例。每个 NSString 实例也一样,无论它的内部字符串如何。  

任何特定的对象是用于以特定的方式而设计的。你可能知道一个字符串对象表示某些字符的字符串，但你不需要知道确切的内部机制，用来存储这些字符。你不懂的内部行为对象本身用于直接处理的特点，但你要知道如何你预期的交互作用与对象，也许是为了索取特定字符或请求一个新的对象，在其中所有原始字符转换为大写。  

在 Objective-C 中，类接口指定一个给定的类型的对象是如何被其他对象使用的。换句话说，它定义了类的实例与外部世界之间的公共接口。

###可变性决定了一个代表值能否被取代 - Mutability Determines Whether a Represented Value Can Be Changed 
一些类定义对象是不可变的。这意味着当一个对象创建，并且随后不能由其他对象更改时，必须设置内部内容。在 Objective-C 中，所有基本的  NSString  和  NSNumber  对象都是不可变的。如果您需要代表一个不同的数字，则必须使用一个新的  NSNumber  实例。  

不可变的类还提供了一个可变的版本。如果您一定需要更改在运行时的字符串内容，例如他们在收到通过网络连接时填加字符，您可以使用 NSMutableString 类的一个例子。这个例子像 NSString 对象一样，除此之外他们还提供更改此对象表示的字符。  

虽然  NSString  和  NSMutableString  是不同类，但他们有许多相似之处。你并不需要从零开始的编写两个独立类，只是有时候碰巧有一些类似的行为要写两个完全独立的类，它完全可以利用现有的东西完成。  

###类的继承 - Classes Inherit from Other Classes
在自然的世界里，将动物分为像种、 属、族这样的各个门类。这些群体是分层的，许多的物种可能都属于同一属，许多的属可能同是一个族。  

举个例子，猩猩、狒狒和人类有明显的相似性。虽然他们都属于不同的物种，和甚至不同的属，部落和亚科，但是它们分类学相关，因为它们都属于同一个族 （称为"人科"），如图 1-1 所示。   

![图1-1  物种之间的分类关系](C:/Users/asusa/Pictures/1-1.png)  
在全世界的面向对象的编程中，对象则是也分成为各层次的组。对象被简单的分成许多类，并不会为了像 genus 、 species 这样不同的层次使用不一样的术语。同样的，人类作为人科家族成员继承着某些特征，那么就可以在从父母类功能性的传承中建立某一类。 

当一个类从另一个类有所继承时，新的类就会继承旧类的全部行为和属性。它也有机会来定义它自己的其他的行为和属性，或也可以重写继承来的行为属性。  

在 Objective-C 字符串类的情况下， NSMutableString 描述指定的类继承于 NSString ，如图 1-2 所示。所有由 NSString 提供的功能都是可用于 NSMutableString 的，如查询特定的字符或要求更改新的大写字符串，但 NSMutableString 添加了可以让您附加、 插入、 替换或删除子字符串和单个字符的方式。  

!图 1-2  NSMutableString 的继承
###The Root Class提供基本的功能 - The Root Class Provides Base Functionality
所有生物体都拥有着一些基本的" life "特点，有些功能对于 Objective-C 中的对象是很常见的。

当 Objective-C 对象需要使用另一个类的一个实例时，它需要其他类提供一定的基本特征和行为。为此， Objective-C 定义根类从中绝大多数的其他类继承，称为 NSObject 。当一个对象遇到另一个对象时，它将至少能够使用  NSObject  类描述所定义的基本行为进行交互。  

当您定义您自己的类时，你应该至少从 NSObject 中继承。一般情况下，你应该找一个提供你所需最接近的功能的 Cocoa or Cocoa Touch 对象，然后从其中继承。  

如果您想要在 iOS 应用程序中使用自定义的按钮，提供的 UIButton 类不能提供足够可自定义的属性以满足您的需要，从 NSObject 中创建一个新类比从 UIButton 中创建更有意义。如果你只是从 NSObject 简单的继承，你将需要由 UIButton 类定义的所有复杂的视觉交互和通信，这只是为了让你的行为方式按照用户的期望的按钮定义来实现。此外，通过从 UIButton 继承，你的子类会自动地获得任何未来的功能增强或可能应用于内部 UIButton 行为的 bug 修复。  

UIButton 类本身定义继承 UIControl ，描述了在 iOS 上所有用户界面控件的常见基本行为。反过来， UIControl 类继承 UIView ，给在屏幕显示的对象提供常用功能。UIView 继承于UIResponder，允许它响应用户输入，如水龙头、 手势。最后，也是最重要的，UIResponder 继承 NSObject ，图 1-3 所示。

!图 1-3  UIButton 类的继承

这一连串的继承是指 UIButton 任何自定义子类将不仅是继承声明了 UIButton 本身的功能，也依次从每个超类继承功能。你会最终以一个像按钮的对象结束，它可以在屏幕上自我显示、 对用户输入作出响应以及与所有基本的 Cocoa Touch 对象进行通信。 

对于你需要使用的类，要把它的继承链牢记于心，以便它可以把它所有能做的做好。类参考文档提供的 Cocoa and Cocoa Touch 允许从任何类可以轻松导航到每个超类。如果你在一个类接口或引用中找不到你需要的，它可能很好的在进一步的超类中定义了。  

##类接口定义预期交互 - The Interface for a Class Defines Expected Interactions
面向对象编程的诸多好处之一就是前面提到的想法 — —要使用一个类，那么你所需要知道的就是如何与它的实例进行交互。更具体地说，应该设计一个让对象隐藏其内部实现的细节。

如果你在 iOS 应用程序中使用标准的 UIButton ，你不需要担心像素在屏幕上如何操纵按钮来显示。你需要知道的就是您可以更改某些属性，比如按钮的标题和颜色，并当你将它添加到您可视化界面时表示信任，它将会以你期望的方式正确显示。

当您定义您自己的类时，您需要先搞清楚这些类的公共属性和行为。你想访问哪些公开属性？你应该让这些属性改变吗？其他对象与您的类的实例如何沟通？

此信息进入您的类的接口 — — 它定义了你打算与你的类的实例中的其他对象进行交互的方式。公共界面由您的类的内部行为进行独立描述，它组成了类。在 Objective-C 中，接口和安装通常放置在独立的文件中，这样你只需要使接口开放。

###基本语法 - Basic Syntax
在 Objective-C 中描述一个类接口的语法如下所示：
```
@interface SimpleClass : NSObject
 
@end
```
本例声明了一个从 NSObject 中 继承来的名为  SimpleClass 的类。

@interface  声明内部定义的公共属性和行为。在此示例中，没有指定属性或行为超出超类，所以唯一的可在 SimpleClass  上实现的实例预计功能是从 NSObject 继承来的。
###属性控制对对象值的访问 - Properties Control Access to an Object’s Values
对象通常具有属性供公众查阅。例如，如果您在一款记录保存软件中定义了一个类来表示人，那你可能需要一个决定字符串来表示一个人的姓和名的属性。

这些属性的声明应添加内部接口，像这样：
```
@interface Person : NSObject
 
@property NSString *firstName;
@property NSString *lastName;
 
@end

```
在此示例中，Person  类声明了两个公共属性，这两个属性是  NSString  类的实例。

这两个属性都是对 Objective-C  的对象而言的，所以他们使用星号以表明它们是  C  指针。他们也像在  C 语言中其他变量的声明语句一样，需要以分号结尾。

您可能会决定添加一个属性来表示一个人出生日期，以便可以按年龄给人分组，而不是只按名称进行排序。你可以对一个数字对象使用这样的属性：
```



