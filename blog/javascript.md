### Book

《JavaScript入门经典》清华出版社

### 导入模块

```javascript
import React from 'react';
```



### Classs用法 - ES6

> **class 知识点**

- 类和模块默认就是严格模式，不需指定 “use strict”，ES6把整个语言升级到了严格模式；
- 类不存在变量提升，所以类定义要写在调用，继承之前！

- class中的 this 代表实例对象
- ES5 中的构造方法对应于 ES6 中的构造方法
- 类中熟悉感以及方法除非使用 this 绑定到实例，否则都是定义在 prototype 上面。

```javascript
let methodName = "getName";
class Animal{
    // 构造方法
    constructor(name){
        this.name = name;
    }
    // 方法
    eat(){
        console.log(this.name+" is eating something.");
    }
    // 通过表达式获得类的方法名：getName
    [methodName](){
        return this.name;
    }
}
```

>  constructor方法

- constructor（）通过 new 命令生成实例时自动调用该方法。
- 默认返回实例对象，即 this 。
- class 定义的类必须通过 new 调用，否则报错；

> class中方法

- 不用加“ function ”关键字，方法之间不用逗号隔开
- 所有的方法都是定义在原型对象上面的！ " Animal.prototype.eat "
- 通过 **Object.assign()** 方法可以一次向类添加多个方法
  - 延伸：Object.assign可以用来实现对象拷贝，返回目标对象。

```javascript
class Point{
    constructor(){ //...}
}

Object.assgin( Point.prototype,{
	toString(){},
     toValue(){}
})
```

> class 表达式

- 类名为 MyClass，Me 只在 类的定义中使用，不需要可以省略；

```javascript
const MyClass = class Me{
    getClassName(){
        return Me.name;
    }
}
```

> 私有属性 #x



> **this 指向**
>
> ```javascript
> class Animal{
>     constructor(name){
>         this.name = name;
>     }
>     eat(){
>         console.log(this.name+" is eating something.");
>     }
> }
> let cat = new Animal('coco');
> let {eat} = cat;
> eat();  // 报错，全局调用eat（），this指向window，不存在 name 属性；
> ```
>
> **解决**
>
> - 构造函数中绑定到this
>
>   ```javascript
>   constructor(name){
>       this.name = name;
>       this.eat = this.eat.bind(this);
>   }
>   ```
>
> - 构造函数中定义：箭头函数
>
>   解释：箭头函数的 this 绑定到定义所在的环境
>
>   ```javascript
>   constructor(name){
>       this.name = name;
>       this.eat = (name=" there")=>{
>           console.log(this.name+" is eating something.");
>       }
>   }
>   ```
>
> - proxy
>
>   ```javascript
>   
>   ```



### Date

```javascript
new Date()/toLocalString(); // 2018/9/13 下午10:07:11
```

### 定时器

> setInterval()
>
> setTimeOut()

### 跨域问题

跨域问题的出现是因为“同源策略”，出于安全考虑，javascript只能操作相同协议、端口以及域名中的资源或请求。

通过XHR实现Ajax通信:

```javascript
var request = new XMLHttpRequest();  // 源自 HTTP API
```

- JSONP，json with padding，参数式json。

  - 服务器端的响应采用JSON编码的数据格式，执行脚本时，js解析器能自动将其解码。

  ```javascript
  var script = document.createElement("script"); // script标签跟img元素，有能力不受限制地从其他域加载资源；
  script.src = "http://freegeoip.net/json/?callback=handleResponse";
  document.body.insertBefore(script,document.body.firstCgild);
  ```

- CORS，Cross-Origin Resource Share，跨源资源共享。

  - 用新的“Origin”请求头和新的“Access-Control-Allow-Origin”响应头来扩充http。
  - 定义了在访问跨域资源时，浏览器跟服务器该如何沟通。

- document.domain

  - 问题：同源问题会给使用多个子域的大站点带来问题。

  - 解决：把两个窗口包含的脚本的domain设置成相同的值，name这两个窗口就不再受同源策略的约束了。

    ```javascrip
    home.example.com
    orders.example.com
    
    document.domain = example.com；
    ```

- postMessage

  - 通过window对象的postMessage发送数据，并在子页面中通过异步onMessage事件取出数据。

  ```javascript
  <iframe src="b.html">
  window.frames[0].postMessage(data,'/');
  
  // b.html的js中
  window.addEventListener("message",data=>{}）
  window.onMessage = function( messageEvent ){...}
  ```

### 集合

- Array
- Object
- Map
- Set



### 对象

创建

- 工厂模式：函数体内部常见obj并返回

- 构造函数模式：每个实例生成方法

- 原型模式

- 组合构造函数模式与原型模式

- 动态原型模式

  ```javascript
  function Cat(name){
      this.name = name;
      if( typeof Cat.sayName != "function"){
          Cat.prototype.sayName = function(){
              alert(this.name);
          }
      }
  }
  ```

  

### 继承

- 原型链继承
- 寄生组合继承：优点：改变子类原型不会改变父类原型；父类实例属性与方法初始化一遍。

```javascript
function Animal(){
	this.name = "animal";
}
Animal.prototype.say = function(){
	alert("say something");
};

function Cat(){
	Animal.call(this);

	(function(){
		vat Temp = function(){};
		Temp.prototype = Animal.prototype;
		Cat.prototype = new Temp();
	})();
}

var cat = new Cat();
```



实例继承

原型继承

### 原型链

描述



### 问题

- 描述：setTimeout 返回闭包，this指向全局window

```javascript
window.onload = function(){

	name = "阿肆";
	var cat = new Cat("Kitty");
	cat.sayName();
	setTimeout((new Cat("Kitty")).sayName, 2000); // 返回闭包，显示“阿肆”
}

function Cat(name){
    this.name = name;
    if( typeof Cat.sayName != "function"){  // 动态原型模式
        Cat.prototype.sayName = function(){
            alert(this.name);
        }
    }
}
```

