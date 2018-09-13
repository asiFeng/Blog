## 走了很远，还是会开始

### 害怕，跟怀疑同行

#### 除此，别无它物

##### 希望有人一起

------



[React中文教程](https://react.docschina.org/docs/hello-world.html)

### Hello world

```jsx
ReactDom.render(
    <div>
        <h1>Hello World!</h1>
    </div>,
    document.querySelector("root")
);
```

建议先了解ES6中：

[箭头函数](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/Arrow_functions)， [类](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Classes)， [模板字符串](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Template_literals)， [`let`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/let)， 和 [`const`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/const) 声明 

### JSX简介

> jsx是javascript的扩展语言，在React中推荐使用，看起来比较像模板语言。
>
> 使用小驼峰命名，className...

```jsx
const user = {
    firstName: "Jone",
    lastName:  "Snow"
};

const element = <h1>Hello, 阿肆！</h1>;
const userElement = (
    <div>Hello, {user.firstName} {user.lastName}</div>
);
```

> Basel编译器会把 JSX 编译成 React.createElement(...) 的方法调用。

```jsx
// 方法一
const element = (
    <div className="react-item">react对象</div>
);

// 方法二  等同于
Render.createElement(
    'div',
    {className: 'react-item'},
    'react 对象'
);
```

### react元素

> 元素是构成react的最小单位，用来描述你在屏幕上看到的最小单位。React当中的元素事实上是普通的对象，React DOM可以确保浏览器DOM 的数据与React元素保持一致。

```jsx
// 方法二将返回如下类似的“react元素”，react通过读取这些对象来构建DOM并保持数据一致；
const element = {
    type: 'div',
    props: {
        className: 'react-item',
        children: 'react对象'
    }
}；
```

> 在页面上定义react 根节点 “ \<div class="root"\>\</div\> ”，然后通过“ ReactDOM.render( reactElement，根节点Dom元素) ”将其渲染到页面上。

- react元素都是immutable不可变的。
- react只会更新必要的部分。

### 组件 & Props

> 组件化开发思想，将UI切分成一些独立可复用的组件，再组装起来。
>
> **组件名字必须大写！且有结束标识 \< Welcome  /\>**
>
> **组件的返回值中智能有一个根组件，所以必须用div标签包裹所有子元素**

- 组件输入：props
- 组件输出：React元素

```jsx
// 函数定义组件
function Welcome(props){
  return (<div>Welcome {props.name}</div>);
}
ReactDOM.render(
  <Welcome name="函数定义组件" />,
  document.getElementById("root2")
);

// ES6 类定义组件
class Animal extends React.Component{
  render(){
    return (
        <h1 className="root4">
            Animal: {this.props.name}    <!--注意参数传入方式-->
        </h1>
    );
  }
}

ReactDOM.render(
  <Animal name="ES6 类定义组件" />,  // 组件使用
  document.getElementById("root3")
);
```

![两种组件定义使用结果](./assets/react定义组件.PNG)

```jsx
// 组件套用
function SaySomething(props){
    return (
        <div>SaySomething
            <Welcome name="组件套用" />
        </div>
    );
}
```

### State & 生命周期

> 现阶段学习中，我们通过 ReactDOM.render( ) 来更新UI。

- 定义为类的组件有一些特性。局部状态即是如此，只适用于类。

```jsx
// 通过状态来刷新时间
class Clock extends React.Component{
     // 构造函数
    constructor(props){    
        super(props);
        this.state = { data: new Date() };  // 初始化状态
    }
    
    render(){
        return (<h1>{ this.state.date.toLocaleString() }</h1>);
    }
    
    // 组件挂载好以后执行
    componentDidMount(){     
        this.timerId = setInterval( ()=> this.tick(),1000);
    }
    
    // this.setState() 设置状态，只能通过此方法改变
    tick(){             
        this.setState( { data:new Date() } );
    }
    
    // 组件即将销毁时清除定时器
    componentWillUnmount(){   
        clearInterval(this.timerId);
    }
}

ReactDOM.render(<Clock />, document.querySelector("#timer"));
```

> **知识点**
>
> 

# Question

React中的核心概念

- diff算法
- 虚拟DOM

组件状态

- 无状态组件，通过js函数创建，呈现数据
- 有状态组件，通过class创建，有业务逻辑，需要操作数据，需要使用state。

#### JavaScript函数创建

- 注意：1 函数名称必须为大写字母开头，React通过这个特点来判断是不是一个组件
- 注意：2 函数必须有返回值，返回值可以是：JSX对象或`null`
- 注意：3 返回的JSX，必须有*一个*根元素
- 注意：4 组件的返回值使用`()`包裹，避免换行问题

#### class创建

> 在es6中class仅仅是一个语法糖，不是真正的类，本质上还是构造函数+原型 实现继承

// - **ES6中的所有的代码都是运行在严格模式中的**
// - 1 它是用来定义类的，是ES6中实现面向对象编程的新方式
// - 2 使用`static`关键字定义静态属性
// - 3 使用`constructor`构造函数，创建实例属性
// - [参考](http://es6.ruanyifeng.com/#docs/class)

### 组件生命周期

- mounting
- updating
- unmounting

？？？使用类就允许我们使用其它特性，例如局部状态、生命周期钩子 ？？？

[别人blog01](https://segmentfault.com/a/1190000012921279)

















###### 