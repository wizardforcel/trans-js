# `第 3 章：C++：架起过程式编程与面向对象编程的桥梁`

## `3.1 从 C 到 C++ 的演变`

`C++` 的发展标志着编程语言的一次重大进化，架起了过程式编程与面向对象编程（OOP）之间的桥梁。在这一部分，我们将探索从 `C` 到 `C++` 的历程以及定义 `C++` 作为一种多功能强大语言的核心概念。

`1\. C++ 的起源：`

`C++` 由 `Bjarne Stroustrup` 在 1980 年代初期创建，作为 `C` 编程语言的扩展。`Stroustrup` 的目标是将 `C` 的高效性和低级功能与高级特性相结合，从而实现更结构化和模块化的代码。

`#include <iostream>`

`int main()  {`

`std::cout <<  "Hello, C++!"  <<  std::endl;`

`return  0;`

`}`

`2\. 面向对象编程（OOP）：`

`C++` 与 `C` 的一个基本区别是引入了面向对象编程（OOP）。在 `C++` 中，你可以定义类和对象，将数据和行为封装成可重用和组织良好的单元。

`class Rectangle {`

`public:`

`int width;`

`int height;`

`int area()  {`

`return width * height;`

`}`

`};`

`int main()  {`

`Rectangle rect;`

`rect.width =  5;`

`rect.height =  10;`

`int area = rect.area();`

`return  0;`

`}`

`3\. 类和对象：`

`C++` 中的类作为创建对象的蓝图。它们封装了操作数据的属性（数据）和方法（函数）。对象是类的实例。

`4\. 继承：`

`C++` 支持继承，允许基于现有类创建新类。继承实现了代码重用和类层次结构的构建。

`class Square :  public Rectangle {`

`public:`

`Square(int side)  {`

`width = side;`

`height = side;`

`}`

`};`

`5\. 多态：`

`C++` 中的多态允许不同类的对象被视为公用基类的对象。这促进了动态方法调用和运行时的灵活性。

`class Shape {`

`public:`

`virtual  void draw()  {`

`// 默认实现`

`}`

`};`

`class Circle :  public Shape {`

`public:`

`void draw()  override  {`

`// 绘制圆形`

`}`

`};`

`6\. 封装：`

`C++` 支持封装，将类的内部细节隐藏起来，仅暴露必要的部分。访问控制符如 `public`、`private` 和 `protected` 控制类成员的可见性。

`class BankAccount {`

`private:`

`double balance;`

`public:`

`void deposit(double amount)  {`

`if  (amount >  0)  {`

`balance += amount;`

`}`

`}`

`double getBalance()  {`

`return balance;`

`}`

`};`

`7\. 模板：`

`C++` 引入了模板，支持泛型编程。模板使得你可以编写能够处理不同数据类型的代码，同时保持类型安全。

`template  <typename T>`

`T add(T a, T b)  {`

`return a + b;`

`}`

`8\. 标准模板库（STL）：`

STL是C++中一组预定义的类和函数，用于处理常见的数据结构（如向量、列表和映射）和算法。它简化了复杂任务并促进了代码重用。

`#include <vector>`

`#include <algorithm>`

`int main()  {`

`std::vector<int> numbers =  {5,  2,  8,  1,  9};`

`std::sort(numbers.begin(), numbers.end());`

`return  0;`

`}`

`从C到C++的演变带来了丰富的功能和编程范式，使得C++成为一种多用途语言，适用于各种应用。它能够无缝地结合过程式编程和面向对象编程，这也促成了它在软件开发中的持久流行。理解C++的核心概念对于充分利用其在现代编程中的潜力至关重要。`

`***`

## `3.2 C++中面向对象编程的核心概念`

`面向对象编程（OOP）是C++中的一种基础范式，使开发者能够创建更有组织、模块化和可维护的代码。在这一部分中，我们将深入探讨C++中应用的OOP核心概念。`

`1\. 类和对象:`

`面向对象编程（OOP）的核心是类和对象。类是创建对象的蓝图。它定义了描述对象行为和属性的属性（数据成员）和方法（函数）。`

`class Circle {`

`public:`

`double radius;`

`double calculateArea()  {`

`return  3.14159  * radius * radius;`

`}`

`};`

`在这个例子中，Circle是一个类，拥有一个radius属性和一个方法calculateArea()，用于计算圆的面积。`

`2\. 封装:`

`封装是将数据（属性）和对数据进行操作的方法（函数）捆绑在一个类中的做法。在C++中，你可以通过访问说明符来控制类成员的可见性：public、private和protected。`

`class BankAccount {`

`private:`

`double balance;`

`public:`

`void deposit(double amount)  {`

`if  (amount >  0)  {`

`balance += amount;`

`}`

`}`

`double getBalance()  {`

`return balance;`

`}`

`};`

`这里，balance属性被封装为private，这意味着它只能通过public方法deposit()和getBalance()进行访问和修改。`

`3\. 继承:`

`继承允许你基于现有的类（基类或超类）创建新类（派生类或子类）。派生类继承基类的属性和方法，促进了代码重用和层次结构的建立。`

`class Shape {`

`public:`

`virtual  double calculateArea()  {`

`return  0.0;  // 默认实现`

`}`

`};`

`class Circle :  public Shape {`

`public:`

`double radius;`

`double calculateArea()  override  {`

`return  3.14159  * radius * radius;`

`}`

`};`

`在这个例子中，Circle是Shape的派生类，并重写了calculateArea()方法以提供自己的实现。`

`4\. 多态性:`

`多态性允许不同类的对象被视为公共基类的对象。这促进了动态方法调用和运行时灵活性。`

`Shape* shape =  new Circle();`

`double area = shape->calculateArea();`

`这里，Circle对象被视为Shape对象，并相应地调用calculateArea()方法。`

`5\. 抽象：`

`抽象是通过将复杂系统建模为具有特定行为和属性的对象来简化系统的过程。类通过封装相关细节提供了一种抽象层次。`

`class Car {`

`public:`

`virtual  void start()  =  0;`

`virtual void stop() = 0;`

`};`

`class ElectricCar : public Car {`

`public:`

`void start() override {`

`// 启动电动汽车`

`}`

`void stop() override {`

`// 停止电动汽车`

`}`

`};`

-   在这个例子中，`Car`是一个抽象类，具有两个纯虚函数，强制派生类如`ElectricCar`必须提供`start()`和`stop()`的实现。

`6. 组合：`

-   组合是通过将更简单的对象作为属性组合来构建复杂对象的实践。它促进了代码的模块化和可重用性。

`class Engine {`

`public:`

`void start() {`

`// 启动发动机`

`}`

`void stop() {`

`// 停止发动机`

`}`

`};`

`class Car {`

`private:`

`Engine engine;`

`public:`

`void start() {`

`engine.start();`

`}`

`void stop() {`

`engine.stop();`

`}`

`};`

-   在这个例子中，一个`Car`包含一个`Engine`作为属性，允许它将任务委托给`Engine`对象。

-   理解这些核心的面向对象编程概念在C++中对于设计和开发结构化和模块化的软件至关重要。这些概念为构建复杂和可维护的系统提供了基础，并广泛应用于各种应用中，从游戏开发到企业软件。

`***`

## `3.3 内存管理：从 Malloc 到构造函数`

-   内存管理是C++编程的一个关键方面，与C显著不同，因为引入了类和对象。在本节中，我们将探讨C++如何管理内存，包括构造函数和析构函数的使用。

`1. 构造函数：`

-   在C++中，构造函数是定义在类中的特殊成员函数，当创建类的对象时会被调用。构造函数初始化对象的属性，并在必要时分配资源。

`class Student {`

`public:`

`Student() {`

`// 构造函数`

`age = 0;`

`name = "Unknown";`

`}`

`private:`

`int age;`

`std::string name;`

`};`

-   在这个例子中，`Student`类有一个构造函数，当创建`Student`对象时，会为`age`和`name`属性设置默认值。

`2. 析构函数：`

-   析构函数是另一个特殊的成员函数，当对象超出作用域或被显式删除时被调用。析构函数用于释放对象分配的资源，例如动态内存或文件句柄。

`class FileHandler {`

`public:`

`FileHandler(const std::string& filename) {`

`// 构造函数：打开文件`

`file.open(filename);`

`}`

`~FileHandler() {`

`// 析构函数：关闭文件`

`file.close();`

`}`

`private:`

`std::ifstream file;`

`};`

-   在这个例子中，`FileHandler`类有一个构造函数，用于打开文件，并且在对象被销毁时有一个析构函数，用于关闭文件。

`3. 动态内存分配：`

-   C++提供了如`new`和`delete`这样的操作符用于动态内存分配和释放。当您使用`new`创建对象时，它的构造函数被调用，并在堆上分配内存。

`Student* studentPtr = new Student(); // 动态对象创建`

-   要释放内存并调用析构函数，您可以使用`delete`：

`delete studentPtr;  // 析构函数被调用，内存被释放`

4\. `RAII`（资源获取即初始化）：

`RAII`是C++编程习惯，它将资源（如内存或文件句柄）的生命周期与对象的生命周期绑定在一起。构造函数获取资源，析构函数释放资源，确保资源得到适当管理。

`class DatabaseConnection {`

`public:`

`DatabaseConnection() {`

`// 构造函数：打开数据库连接`

`}`

`~DatabaseConnection() {`

`// 析构函数：关闭数据库连接`

`}`

`};`

使用`RAII`，资源管理变得自动和确定，最小化了资源泄漏的风险。

5\. 复制构造函数：

C++提供了复制构造函数，用于创建现有对象的副本。默认情况下，C++生成一个执行逐成员复制的复制构造函数。然而，您可以定义自定义复制构造函数，以确保资源的正确复制。

`class MyString {`

`public:`

`MyString(const MyString& other) {`

`// 自定义复制构造函数`

`data = new char[strlen(other.data) + 1];`

`strcpy(data, other.data);`

`}`

`private:`

`char* data;`

`};`

在这个例子中，`MyString` 类定义了一个自定义复制构造函数，以创建字符数据的深拷贝。

理解 C++ 中的内存管理对于创建健壮和资源高效的程序至关重要。构造函数和析构函数在资源管理中起着关键作用，而 `RAII` 习惯用法鼓励资源管理的最佳实践。通过有效使用这些特性，C++ 开发人员可以确保在对象生命周期内正确分配和释放内存及其他资源。

* * *

## 3.4 标准模板库（`STL`）

标准模板库（`STL`）是 C++ 的核心组件，提供了一组预定义的类和函数，用于常见数据结构和算法。它通过提供一组经过良好测试和高效的组件，简化复杂任务并促进代码重用。在本节中，我们将探索 `STL` 的一些关键组件。

1\. 容器：

`STL` 提供了几种容器类，以高效存储和管理数据。一些常用的容器包括：

•            `Vector`: 一个动态数组，在添加或删除元素时自动调整大小。

•            `List`: 一个双向链表，允许在列表的任何位置高效插入和删除元素。

•            `Map`: 一个关联容器，存储键值对，通过键提供快速查找。

•            `Set`: 存储唯一元素的容器，用于维护一组不同的值。

`#include <vector>`

`#include <map>`

`std::vector<int> numbers = {1, 2, 3, 4, 5};`

`std::map<std::string, int> ageMap;`

2\. 迭代器：

迭代器用于遍历和操作容器中的元素。它们提供了一种统一的方式来访问元素，无论底层容器类型如何。

`for (auto it = numbers.begin(); it != numbers.end(); ++it) {`

`// 使用 'it' 访问或修改元素`

`}`

`3. 算法：`

STL 包含了一系列操作容器的算法。这些算法执行排序、查找和修改元素等任务。一些常用的算法包括：

• `std::sort`: 用于对容器中的元素进行排序。

• `std::find`: 在容器中查找元素。

• `std::for_each`: 对容器中的每个元素应用一个函数。

`#include <algorithm>`

`std::sort(numbers.begin(), numbers.end());`

`auto result = std::find(numbers.begin(), numbers.end(), 3);`

`4. 函数对象（函数对象）：`

函数对象是表现得像函数的对象。它们通常与算法一起使用，以自定义它们的行为。你可以通过重载 `operator()` 来定义自己的函数对象。

`struct Square {`

`int operator()(int x) const {`

`return x * x;`

`}`

`};`

`std::transform(numbers.begin(), numbers.end(), numbers.begin(), Square());`

`5. 字符串：`

`C++` 提供了 `std::string` 类作为 STL 的一部分，提供了比 C 风格字符数组更易用且多功能的替代方案。`std::string` 负责内存管理，并提供了各种字符串操作函数。

`#include <string>`

`std::string greeting = "Hello, World!";`

`6. 智能指针：`

STL 包括智能指针，如 `std::shared_ptr`、`std::unique_ptr` 和 `std::weak_ptr`，用于高效地管理动态内存。当对象不再需要时，这些指针会自动处理内存释放，减少内存泄漏的风险。

`#include <memory>`

`std::shared_ptr<int> sharedPtr = std::make_shared<int>(42);`

`std::unique_ptr<double> uniquePtr = std::make_unique<double>(3.14);`

`7. 实用功能：`

STL 提供了像 `std::pair` 和 `std::tuple` 这样的实用功能，用于处理值的对和元组。这些常用于返回多个值的函数和算法中。

`#include <utility>`

`std::pair<int, std::string> person = std::make_pair(25, "Alice");`

`std::tuple<int, double, std::string> data = std::make_tuple(42, 3.14, "Hello");`

标准模板库（STL）是`C++`开发人员的强大工具，提供了一系列可重用的组件和算法，简化了常见的编程任务。通过有效地利用STL，程序员可以编写更高效、更易维护的代码，减少在数据结构和算法方面的重复劳动。理解STL的组成部分及其使用方法对于任何`C++`开发人员来说都是必不可少的。

* * *

## `3.5 C++的现实世界应用`

`C++`是一种多用途的编程语言，以其性能和效率著称。在本节中，我们将探讨`C++`的一些现实世界应用，并介绍它在各个领域的使用。

`1. 系统编程：`

`C++广泛用于系统编程任务，尤其在开发操作系统、设备驱动程序和嵌入式系统固件时起着至关重要的作用。其低级别的能力使其适合管理硬件资源并与外设进行交互。`

`// C++中系统编程的示例`

`#include <iostream>`

`#include <fstream>`

`#include <unistd.h>`

`int main() {`

`std::cout << "你好，C++系统编程！" << std::endl;`

`std::ofstream outputFile("data.txt");`

`outputFile << "数据已写入文件。" << std::endl;`

`close(1); // 关闭标准输出`

`return 0;`

`}`

`2. 游戏开发：`

`C++因其性能和处理资源密集型任务的能力而成为游戏开发的热门选择。像虚幻引擎（Unreal Engine）和Unity等游戏引擎在其核心系统中广泛使用C++。`

`// C++ 游戏开发`

`#include <iostream>`

`class Game {`

`public:`

`void run() {`

`// 游戏循环`

`while (isRunning) {`

`// 游戏逻辑和渲染`

`}`

`}`

`private:`

`bool isRunning = true;`

`};`

`3. 高性能计算（HPC）：`

`C++在高性能计算领域备受青睐，在需要最大计算能力的情况下尤为重要。C++的低级内存控制和优化能力使其适用于科学仿真、气象建模和金融分析等任务。`

`// C++中的高性能计算`

`#include <iostream>`

`#include <vector>`

`#include <omp.h>`

`int main() {`

`std::vector<double> data(1000000, 0.0);`

`#pragma omp parallel for`

`for (int i = 0; i < data.size(); ++i) {`

`data[i] = i * 2.0;`

`}`

`std::cout << "HPC任务完成。" << std::endl;`

`return 0;`

`}`

`4. 航空航天和国防：`

`C++在航空航天和国防行业中被用于飞行控制系统、雷达信号处理和仿真软件等任务。其可靠性和实时能力使其适用于安全关键型应用。`

`// C++中的航空航天应用`

`#include <iostream>`

`class FlightControlSystem {`

`public:`

`void controlFlight() {`

`// 飞行控制逻辑`

`}`

`};`

`5. 金融与交易：`

`在金融领域，C++用于算法交易、风险管理和高频交易系统。其低延迟能力和高效的内存管理对于处理大量金融数据至关重要。`

`// C++中的算法交易`

`#include <iostream>`

`class TradingAlgorithm {`

`public:`

`void execute() {`

`// 交易策略实现`

`}`

`};`

`6. 游戏引擎和图形库：`

`C++是开发游戏引擎和图形库的首选语言。像OpenGL和DirectX这样的库利用C++的性能来创建身临其境的游戏体验。`

`// C++图形编程`

`#include <iostream>`

`#include <OpenGL/gl.h>`

`int main() {`

`// OpenGL渲染代码`

`return 0;`

`}`

`7. 汽车行业：`

`C++用于开发车辆中的嵌入式软件，包括发动机控制单元（ECU）、信息娱乐系统和自动驾驶算法。其实时性能和高效能对于汽车应用至关重要。`

`// C++中的汽车软件开发`

`#include <iostream>`

`class AutonomousDrivingSystem {`

`public:`

`void drive() {`

`// 自动驾驶逻辑`

`}`

`};`

C++的广泛应用证明了它的灵活性和强大功能。它仍然是要求高性能、有效内存管理和低级控制的项目的首选语言。了解C++在不同领域的应用，对于那些希望专注于特定行业或项目的开发者来说非常有价值。

`* * *`
