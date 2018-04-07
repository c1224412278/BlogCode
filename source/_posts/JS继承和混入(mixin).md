---
title: JS继承和混入(mixin)
date: 2017-9-26
tags: [ js ]
categories: js
---

> 学问是经验的积累，才能是刻苦的忍耐

# 关于JS的继承和混合(mixin)相关内容
<!-- more -->
---

## 继承

### 组合继承

```
function SuperType(name) {
    this.name = name
    this.color = ['red']
}

SuperType.prototype.sayName = function() {
    console.log(this.name)
    return this.name
}
function SubType(name, age) {
    SuperType.call(this, name) // 继承父类属性  第一次调用SuperType
    this.age = age
}
SubType.prototype = new SuperType() // 继承父类方法及原型链 第二次调用SuperType
SubType.prototype.constructor = Subtype
SubType.prototype.sayAge = function() {
    console.log(this.age)
    return this.age
}
```

使用组合继承的唯一问题就是会调用两次父类的构造函数，而寄生组合继承则不会这样

### 寄生组合继承


```
function SuperType(name) {
    this.name = name
    this.color = ['red']
}

SuperType.prototype.sayName = function() {
    console.log(this.name)
    return this.name
}
function SubType(name, age) {
    SuperType.call(this, name) // 继承父类属性  第一次调用SuperType
    this.age = age
}
// 继承原型链
let prototype = Object.create(SuperType.prototype) // 创建对象
prototype.constructor = SubType // 增强对象
SubType.prototype = prototype // 指定对象
```

## 混合(mixin)

### 显示混入

```
function mixin(sourceObj, targetObj) {
    for(let key in sourceObj) {
        if(!(key in targetObj)) {
            targetObj[key] = sourceObj[key]
        }
    }
    
    return targetObj
}
```

混入的思想就是：将源对象中的属性`复制`到目标对象上

基于显示混入存在一种变体的`寄生继承`:
```
// "传统的JavaScript类" Vehicle
function Vehicle() {
    this.engines = 1
}
Vehicle.prototype.ignition = function() {
    console.log("Turning on my engine")
}
Vehicle.prototype.drive = function() {
    this.ignition()
    console.log("Steering and moving forward!")
}

// "寄生类" Car
function Car() {
    // 首先 car 是一个Vehicle对象
    let car = new Vehicle()
    
    // 对 car 进行定制
    car.wheels = 4
    // 保存 Vehicle 的 drive 方法
    let superDrive = car.drive
    // 重写 car 的 drive 方法
    car.drive = function() {
        superDrive.call(this)
        console.log("Rolling on all " + this.theels + " Wheels!")
    }
}
```

这种继承感觉上比上面的寄生组合继承还要好一点，少调用了一次`Object.create()`方法，但是抛弃了`new Car()`时创建的对象

### 隐式混入

```
var Something = {
    cool: function() {
        this.greeting = "hello world"
        this.count = this.count ? this.count + 1 : 1
    }
}

Something.cool()
Something.greeting // "hello world"
Something.count // 1

var Another = {
    cool: function() {
        // 隐式的把 Something 混入 Another
        Something.cool.call(this)
    }
}

Another.cool()
Another.greeting // "hello world"
Another.count // 1 (count 不是共享状态)
```