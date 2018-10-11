一个模板引擎，用途：

- web应用，动态页面（可以使用动态信息来生成HTML），通过velocityViewServle等处理；
- et al;

允许使用称为引用的标记语言，这些引用通过 Context object拉取，本质就是一张哈希表，提供get()以及set()方法来获取对象；并将对应的值插入到页面中。也提供流程控制语句，调用任意的java方法，以及其它的文件。

是一种MVC模式，不允许在页面中嵌入java代码。

- 可以用来定义只包含“方法”的“Tool”工具，不包含数据。可以像管道一样格式化数据。
- 事件处理

### VelocityView 

- VelocityViewServlet 
  - 独立渲染 velocity 模板的小型服务器，
  -  [HttpServletRequest](http://docs.oracle.com/javaee/6/api/javax/servlet/http/HttpServletRequest.html), [HttpSession](http://docs.oracle.com/javaee/6/api/javax/servlet/http/HttpSession.html), [ServletContext](http://docs.oracle.com/javaee/6/api/javax/servlet/ServletContext.html),都可以在velocity模板中使用
- VelocityLayoutServlet 
- 通过SLF4J logging
- 'error'模板，请求异常时候显示

### GenericTools

```html
$link.setRelative('search.vm');
<input type="text" name="find" value="$!search.criteria" />
```

### Methods

> ### class AbstractSearchTool
>
> ```java
> @DefaultKey(value="search")
>     @InvalidScope(value={"application","session"})
> public abstract class AbstractSearchTool extends PagerTool(){
>     ...
>     protect executeQuery() // 必须实现
>     public  List getItems( ){ ... }
> }
> 
> ```
>
> ```html
> <form name="search" method="get" action="$link.setRelative('search.vm')">
>     <input type="text" name="find" value="$!search.criteria">
>     <input type="submit" value="Find">
> </form>
> 
> #if( $search.hasItems() )
> Showing $!search.pageDescription<br>
> 	#set( $i = $search.index )
> 	#foreach( $item in $search.page )
> 		${i}.$item<br>
> 		#set ($i = $i + 1)
> 	#end
> 	<br>
> 	#if
> ```
>
> 

### Velocity Template language (VTL)

> Notation 符号
>
> ### Varibles
>
> ```html
> $[!] [{] [a..z, A..Z] [a..z, A..Z, 0..9,_] [}]
> ```
>
> - shorthand notation( 简化符号 ):  $mudSlinger_9
> - silent shorthand notation:  $!mudSlinger_9
> - Formal notation: ${mudSlinger_9}
> - silent formal notation: $!{mudSlinger_9}
>
> #### properties 属性
>
> ```html
> $[!] [{] [a..z, A..Z] [a..z, A..Z, 0..9,_] .[a..z, A..Z][a..z, A..Z, 0..9,_] [}]
> ```
>
> eg: 
>
> - regular notation(常规的符号)： $customer.Address
> - formal notation(正式的符号)： ${purchase.Total}
>
> #### Methods
>
> - 方法名字可以是合法的VTL表达式
>
> ```html
> $customer.getAddress()
> ${purchase.getTotal()}
> $page.setTitle( "My Home Page" )
> ```
>
> #### Directives 指令
>
> ```html
> # [ { ] set [ } ] ( $ref = [ ", ' ]arg[ ", ' ] )
> ```
>
> 解析
>
> - $ref：LHS，表达式左边，是一个变量引用或者属性
> - arg：
>   - 用“ ”引用的变量会进行解析
>   - 用 ‘ ’ 引用的变量不解析，当做字符串使用
>   - 如果 RHS 为null， 则不执行该表达式
>   - 也可以是数学表达式
>
> eg：
>
> ```html
> #set ( $monkey = $bill )
> #set ( $monkey.Friend = 'monica' )  = 123
> #set ( $monkey.Numbers = [1..3] )  // range 范围
> #set ( $monkey.Say = ["not", $my, "fault"] ) // 数组
> #set（ ￥monkey.Map = {"banana":"good", "roast beef": "bad"} ） // 对象
> ```
>
> #### if/ elseif / else
>
>   





























