---
title: JavaScript好用还未火的注解@Decorator
date: 2020-06-03 14:42:48
tags:
  - JavaScript基础
category: JavaScript
---

## Decorator 使用

修饰器（Decorator）是一个函数，用来修改类的行为

### Babel 支持

在使用之前需要先下载 babel 插件

```
npm install @babel/plugin-proposal-decorators --save
```

修改配置 ( 我用的是 webpack,所有只要在 webpack.config.js 的配置中加上这句话就行 )

```
plugins: [
              ["@babel/plugin-proposal-decorators", { legacy: true }],
            ],
```

### Class Decorator

```javaScript
const mixins = (...list) {
  return function (target) {
    Object.assign(target.prototype, ...list);
  };
}

const Foo = {
  foo() { console.log('foo') }
};

@mixins(Foo)
class MyClass {}

let obj = new MyClass();
obj.foo()
```

descriptor 对象
{
value：specifiedFunction,// 置换调用
enumerable: false, // 是否可以枚举（for in 循环能否遍历的到）
configurable: true, // 是否可以配置（是否可以用 delete 删除）
writable: true // 是否可以修改（为 false 的时候，只是修改没起作用，不会报错）
}

### method Decorator

```javaScript
class Math {
  @log
  add(a, b) {
    return a + b;
  }
}

function log(target, name, descriptor) {
  var oldValue = descriptor.value;
  console.log(oldValue, target)
  descriptor.value = function() {
    // 这里把console.log改成另外一个监听的add函数，就是一个简单的观察者模式了
    console.log(`Calling "${name}" with`, arguments);
    return oldValue.apply(null, arguments);
  };

  return descriptor;
}

const math = new Math();

// passed parameters should get logged now
math.add(2, 4);
```

### propty Decorator

```javaScript
class C {
  @readonly(false)
  method() { console.log('cat') }
}

function readonly(value) {
  return function (target, key, descriptor) {
	/**
	* 此处 target 为 C.prototype;
	* key 为 method;
    * 原 descriptor 为：{ value: f, enumarable: false, writable: true, configurable: true }
	*/
    descriptor.writable = value
    return descriptor
  }
}

const c = new C()
c.method = () => console.log('dog')

c.method()
```
