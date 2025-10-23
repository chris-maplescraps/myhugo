+++
title = 'Python Class'
date = 2025-10-22T11:50:48+08:00
draft = false
slug = "b592a03"
description = ""
summary = ""
tags = [ "技术", "开发" ]
categories = [ "tech" ]
cover = ""
author = "MapleScraps"

+++

# Python Class

### 什么是类 :question:

##### :green_book: ​类是一种用户自定义的数据类型，用于描述具有相同属性和方法的对象的集合。

##### Python 类中，可以将属性划分为两大类：**类属性 ( Class Attributes )** |  **实例属性 ( Instance Attributes )**

- #### 🎯 类属性 ( Class Attributes )

  - 类属性是直接在 **类定义体内部**、**但在任何方法外部** 定义的变量

    

    ```python
    class Car:
        # 类属性：所有 Car 实例共享，代表轮子的数量
        number_of_wheels = 4 
    
        def __init__(self, color, brand):
            self.color = color  # 实例属性
            self.brand = brand  # 实例属性
    
    # 访问类属性：
    print(Car.number_of_wheels) # 输出: 4
    
    car_a = Car("Red", "Tesla")
    car_b = Car("Blue", "BMW")
    
    # 实例可以访问类属性：
    print(car_a.number_of_wheels) # 输出: 4
    print(car_b.number_of_wheels) # 输出: 4
    ```

- #### ✨ 实例属性 ( Instance Attributes )

  - 实例属性是在 **方法内部**（ 通常是 `__init__` 方法 ）使用 `self.` 前缀定义的变量

    - ##### 📌 特点

      1. **独立性：** 每个对象实例都拥有自己独立的一套实例属性值。一个实例修改了它的实例属性，不会影响其他实例。
    
      2. **定义时机：** 通常在 `__init__` 方法中定义和初始化。
    
      3. **访问方式：** 必须通过 **实例本身** (`instance.attribute`) 来访问。
    
         
    
    ```python
    class Car:
        number_of_wheels = 4 # 类属性
    
        def __init__(self, color, brand):
            # 实例属性：每个对象都有自己独立的颜色和品牌
            self.color = color  
            self.brand = brand  
    
    car_a = Car("Red", "Tesla")
    car_b = Car("Blue", "BMW")
    
    # 实例属性的值是独立的：
    print(car_a.color) # 输出: Red
    print(car_b.color) # 输出: Blue
    
    # 修改 car_a 的属性，不影响 car_b
    car_a.color = "Green"
    print(car_a.color) # 输出: Green
    print(car_b.color) # 输出: Blue (未变)
    ```

---

##### 🔄 区别总结表

| 特性     | 类属性 Class Attributes              | 实例属性 Instance Attributes                |
| -------- | ------------------------------------ | ------------------------------------------- |
| 定义位置 | 直接在类中定义                       | 通常在 `__init__` 方法中，使用 `self.` 定义 |
| 共享性   | **所有实例共享** 同一份数据          | **每个实例独有** 一份数据                   |
| 用途     | 常量、默认值、或所有实例通用的计数器 | 存储每个实例的 **独特状态**                 |
| 语法     | `ClassName.attribute`                | `self.attribute` (在方法内定义/访问)        |

---

##### Python 类中的函数（ Function ）可以被细分为三种主要类型：

1. **实例方法 ( Instance Methods )**
2. **类方法 ( Class Methods )**
3. **静态方法 ( Static Methods )**

---

##### :one: ​实例方法 ( Instance Methods )

##### 📌 特点

- **第一个参数：** 必须是 `self`，它代表了方法所属的 **实例对象**
- **访问能力：** 它可以完全访问和修改该实例对象的 **所有实例属性**（即 `self.xxx`）
- **用途：** 负责实现与特定对象状态相关的操作（ 例如，你的 `data_syslog` 需要知道是哪个日期和哪个日志文件 ）

```python
class Dog:
    def __init__(self, name):
        self.name = name  # 实例属性

    # 实例方法
    def bark(self, sound):
        # 使用 self.name 访问实例属性
        print(f"{self.name} says {sound}!") 

# 调用：必须通过实例
dog = Dog("Buddy")
dog.bark("Woof") # 输出: Buddy says Woof!
```

:two: ​**类方法 ( Class Methods )**

:green_book: 类方法是使用 `@classmethod` 装饰器定义的方法。

##### 📌 特点

- **第一个参数：** 必须是 `cls` (约定俗成的名称，代表**类本身**)。
- **访问能力：** 它可以访问和修改 **类属性**，但 **不能** 直接访问或修改任何特定实例的属性。
- **用途：** 常见用途是作为 **替代构造函数**，提供不同的方式来创建类的实例。

```python
class Car:
    wheels = 4 # 类属性

    # 类方法
    @classmethod
    def get_wheel_count(cls):
        # 使用 cls.wheels 访问类属性
        return cls.wheels

# 调用：可以通过类或实例
print(Car.get_wheel_count()) # 输出: 4
```

:three: **静态方法 ( Static Methods )**

:green_book: ​静态方法是使用 `@staticmethod` 装饰器定义的方法。

##### 📌 特点

- **第一个参数：** **没有** `self` 或 `cls` 参数。
- **访问能力：** 它既**不能**访问实例属性，也**不能**访问类属性（除非通过完整的类名 `Car.wheels`）。它就像一个普通的函数，只是碰巧被放在类内部以保持代码结构清晰。
- **用途：** 存放与类逻辑相关，但**不需要**访问类或实例数据的工具函数。

```python
class MathUtils:
    # 静态方法
    @staticmethod
    def add(a, b):
        return a + b

# 调用：可以通过类或实例
print(MathUtils.add(5, 3)) # 输出: 8
```

🔄 **区别总结表**

| 方法类型 | 装饰器          | 第一个参数必须是 | 能否访问实例属性 | 能否访问类属性                             | 典型用于                       |
| -------- | --------------- | ---------------- | ---------------- | ------------------------------------------ | ------------------------------ |
| 实例方法 | 无              | self             | 可以             | 可以，通过 <br />self. \_\_class\_\_ .attr | 执行依赖于实例状态的操作       |
| 类方法   | `@classmethod`  | cls              | 不能             | 可以                                       | 替代构造函数，<br />操作类属性 |
| 静态方法 | `@staticmethod` | 无               | 不能             | 不能，<br />除非硬编码类名                 | 工具函数，<br />组织代码逻辑   |

---

#### :green_book: 定义类的语法​

```python
class LogProcess():
    pass
```

#### 什么是 构造方法 :question:

:green_book: `__init__` 方法在 Python 类中扮演着 ***初始化构造方法***  的角色。

```python
class LogProcess():
    def __init__(self, year: int, month: int, date: int):
        self.year = year
        self.month = month
        self.date = date
```



:blue_book: ​科普：

- 当执行 `my_log = LogProcess( )` ，`LogProcess` 类中的 `__init__` 方法会立即执行。



