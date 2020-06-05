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

修饰类就相当于对类进行了一次封装，重新封装的类拥有了指定的函数或执行了指定操作。

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

装饰器第一个参数是类的原型对象,第二个参数是所要装饰的属性名,第三个参数是该属性的描述对象
descriptor 对象
{
value：specifiedFunction,// 置换调用
enumerable: false, // 是否可以枚举（for in 循环能否遍历的到）
configurable: true, // 是否可以配置（是否可以用 delete 删除）
writable: true // 是否可以修改（为 false 的时候，只是修改没起作用，不会报错）
}

修饰函数相当于对指定函数添加了响应事件、回调函数、监听事件。

### propty Decorator

```javaScript

class C {
  @readonly(false)
  methods = "cat";
}

function readonly(value) {
  return function (target, key, descriptor) {
    /**
     * 此处 target 为 C.prototype;
     * key 为 method;
     * 原 descriptor 为：{ value: f, enumarable: false, writable: true, configurable: true }
     */
    descriptor.writable = value;
    return descriptor;
  };
}

const c = new C();
c.methods = "bog";

console.log(c);
```

修饰属性相当于对指定属性添加或者修改了属性对象的访问器属性

### Decorator 优先级，串联

Java 的 Decorator 功能强大，不仅有丰富的 Decorator，而且 Decorator 还可以串联。坏消息：亲测 JavaScript Decorator 不能串联，存在覆盖问题，也就是优先级关系：Method Decorator > Class Decorator。当一个 Method 上定义了 Decorator，则 Class Decorator 则不起作用。

```javascript
const promiseAPIBuilder = (code) => {
  // 模拟生成各种接口
  return new Promise((resolve, reject) => {
    setTimeout(() => {
      if (code === 0) {
        resolve({
          code,
          message: "success",
          data: [],
        });
      } else if (code === 404) {
        reject({
          code,
          message: "接口不存在",
        });
      } else {
        reject({
          code,
          message: "服务端异常",
        });
      }
    }, 1000);
  });
};

const showTipDecoratorBulder = (errorHandler) => (
  target,
  propertyKey,
  descriptor
) => {
  const func = descriptor.value;
  return {
    get() {
      return (...args) => {
        return Promise.resolve(func.apply(this, args)).catch((error) => {
          errorHandler && errorHandler(error);
        });
      };
    },
    set(newValue) {
      return newValue;
    },
  };
};
// ****** 构造一个提示错误的`Decorator`
const showTipDecorator = showTipDecoratorBulder((error) => {
  console.log(`Decorator error 消息提示 : ${error.message}`);
});

// ****** class 写法避开限制
class PageAPI {
  @showTipDecorator
  successAPI() {
    return promiseAPIBuilder(0);
  }
  @showTipDecorator
  error404API() {
    return promiseAPIBuilder(404);
  }
  errorWithoutCatchAPI() {
    return promiseAPIBuilder(500);
  }
}
const api = new PageAPI();

const successAPI = async () => {
  const res = await api.successAPI();
  console.log(res);
  // error 没有 catch
  if (!res) return;
  console.log("接口调用成功后的逻辑1");
};
successAPI();

const error404API = async () => {
  const res = await api.error404API(); // error 没有 catch
  if (!res) return;
  console.log("接口调用成功后的逻辑2");
};
error404API();

const errorWithoutCatchAPI = async () => {
  const res = await api.errorWithoutCatchAPI(); // error 没有 catch
  if (!res) return;
  console.log("接口调用成功后的逻辑3");
};
errorWithoutCatchAPI();
```

Decorator 修饰 API 接口管理文件
