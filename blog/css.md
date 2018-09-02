### 动画

```css
@keyframes myAnimate{   // 用@keyframes 规则创建动画
    from{ background-color:yellow};
    50%{  background-color:orange};
    to{  background-color:red};
}

// 使用
.item01{
    animation: myAnimate 5s;
}
```

### flex 弹性布局

父容器

- flex-direction: row  row-reverse  column  column-reverse  initial  inherit
- flex-wrap: wrap  wrap-reverse  nowrap
- justify-content 主轴：flex-start  center  flex-end  space-around  space-between
- align-items 交叉轴: flex-start  center  flex-end stretch  baseline

子元素

- order： default=0，越小越靠前
- flex-grow: default=0, 有空间也不放大；
- flex-shrink: default=1，空间不够，自动缩小；设为0，则不缩小
- flex-basis: 一行占多少，百分之33%，则占三分之一
- align-self: 交叉轴上布局

**设置flex以后，子元素的float，clear，vertical-align将失效**

```css
.flex-container{
	display: flex;
	flex-direction: row;
	align-items: center;
    flex-wrap: wrap;
	background-color: #a99;
	height: 200px;
}
.flexbox{
	background-color: #afa;
	height: 30px;
	width: 100px;
	border: 1px solid blue;
	text-align: center;
}
.flex01,.flex02,.flex03{ flex-basis:32%; } // 设置第一行显示3个
.flex09{ order:1; }  // 设置第二行逆序显示
.flex08{ order:2; }
.flex07{ order:3; }
.flex06{ order:4; }
.flex05{ order:5; }
.flex04{ order:6; }
```

```html
<!-- Flex 测试 -->
<div class="flex-container">
    <div class="flex01 flexbox">1</div>
    <div class="flex02 flexbox">2</div>
    <div class="flex03 flexbox">3</div>
    <div class="flex04 flexbox">4</div>
    <div class="flex05 flexbox">5</div>
    <div class="flex06 flexbox">6</div>
    <div class="flex07 flexbox">7</div>
    <div class="flex08 flexbox">8</div>
    <div class="flex09 flexbox">9</div>
</div>
```

![实现的效果](./assets\flex.PNG)

### Question：

**第二行如何设置靠右显示  ，不影响第一行？**



# 定位元素

盒子模型：

- 块元素自动填充一整行，设置padding以及margin后，content宽度自动收缩；
- 设置width以后，再设置内外边距，则元素向外扩张；
- margin：只有纵向存在覆盖问题，选较大的值

### Float

- 浮动元素脱离了文档流，其父元素看不到它了，因而也不会包围它，导致塌陷问题。

- 浮动元素的包含快就是其最近的跨级祖先元素

- 浮动元素会生成一个块级框

- 

- **清除浮动**

- overflow: hidden; 

  ```css
  .container{
      overflow: hidden; 
  }
  /*
  	讲解： 1、用来防止父容器被超大元素撑大，可以进行裁剪；
  		  2、强迫父元素包含其浮动的子元素
  */
  ```

- 父元素也浮动，父元素后边的元素设置clear属性

  ```css
  .container{
      display:float;
      float:left;
      width:100%;
  }
  .footer{
      clear:both;
  }
  ```

- 父元素中添加非浮动元素，空div

  ```css
  <div style="clear:both;"></div>
  ```

- 父元素上添加伪元素

  ```css
  <div class="container clearfix"></div>
  
  .clearfix:after{
      content:".";
      display:block;
      clear:both;
      visibility: hidden;
      height:0; // 设置不占高度，否则，隐藏了也会有高度
  }
  ```

#### 其他定位元素

- 定位上下文，即包含块。
- 祖先元素

#### 绝对定位

会从文档流中删除，然后相对于其包含块定位，包含块是最近的position值不为static的祖先元素。一般选择一个祖先元素设置position为relative并且不指定偏移属性。

#### Question：

- relative
- absolute
- fixed



