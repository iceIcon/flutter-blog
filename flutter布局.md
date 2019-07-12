# flutter布局
## 布局widget
> 单个widget布局（容器widget）和多个widget布局（布局widget）

单个是只有一个child,多个widget布局是指children；

## 弹性布局
#### flex
- flex布局 类似css中的flex，需要设定主轴方向;
- mainAxisAlignment, crossAxisAlignment设置对齐方式，有了这个解决很多垂直居中问题；

```js
  return Container(
    child: Flex(children: <Widget>[
      Text('2222'),
      Text('3333')
    ],
    direction: Axis.vertical,
    // 设置主轴上的对齐方式；
    mainAxisAlignment: MainAxisAlignment.center,
    // 设置交叉轴上的对齐方式
    crossAxisAlignment: CrossAxisAlignment.start
  )
  );sAlignment
  )
```
#### Expanded
- Expanded是一个扩展的单widget，用于包裹可扩展的元素，并且只可用于Flex widget。
- 可用flex来设置容器的缩放因子；

```js
  return Container(
    child: Flex(direction: Axis.horizontal,
    children: <Widget>[
      Expanded(child: Text('4444'),flex:2),
      Expanded(child: Text('4442224'),flex:1)
    ],)
  );

``` 
#### Flexible
- Expanded继承自Flexible，和Expanded的区别是，当还有剩余空间时，Expanded会占满剩余空间,属于tidge;Flexible不会，属于loose


## 线性布局

- 线性布局是指水平方向（Row）和垂直方向(Column)上的布局，这两个widget都继承至flex,所以大致用法上和flex相似；
- **特殊注意点：** 当多个Row或者Column嵌套时，外面的widget会尽可能占用更多的空间，内部的widget就只是本空间。
- **特殊注意点：** 当有Expanded布局时，Row设置的主轴方向对齐就会失效，代码如下。**大致原因：** 如果mainAxisSize值为MainAxisSize.min，则此属性无意义，因为子widgets的宽度等于Row的宽度。只有当mainAxisSize的值为MainAxisSize.max时，此属性才有意义
```js
  return Container(
    child: Row(
      mainAxisAlignment: MainAxisAlignment.center,
      children: <Widget>[
      Expanded(child: Text('2222')), 
      Text('sssss')
    ],
    ),
  );
```

## 流式布局
- 如Flex,Row,Column，当子widget超出主轴时，就会导致页面出现黄条，这时就可以使用流式布局Wrap来解决。Wrap会把超出的部分换行来处理。

```js
  return Container(
    child: (
      Wrap(children: <Widget>[
        Text('hello world' * 100)
      ],)
    )
  );
```

## 层叠布局
- 层叠（Stack），可以使得子widget层叠在一起，同时子widget是相对于父widget的四个方向来决定定位的。有点类似于前端的absolute的定位形式。

```js
  return Stack(children: <Widget>[
    Image.asset('asset/icon/product1.png'),
    Text('222222')
  ]);
```

## 布局类的--特殊widget

#### Padding
- 可以设置内边距的widget，对子widget起作用；
 
```js
  return Padding(
    padding: EdgeInsets.only(left: 100),
    child:Text('222221112')
  );
```

#### Container
- 可以设置大小，定位，绘制的一个容器widget。

```js
  return Container( 
      child: Text('44444'),
      margin: EdgeInsets.fromLTRB(10,20,30,40),
      padding: EdgeInsets.all(10),
      color: Colors.red,
      alignment: Alignment.bottomCenter,
      decoration: new BoxDecoration(
	      border: new Border.all(color: Colors.red,width:10),
	      color: Colors.white,
	      borderRadius: new BorderRadius.circular(2)
    ),
  );
```

- 如上所示，需要设置border，可以选择Container的decoration属性，实例化的BoxDecoration的border属性来设置边框。

#### Center
- 可以设置子widget居中；继承自align,设置alignment为center的一个封装过的widget。

```
  return Center(child: Text('22222222'),);
``` 

## flutter布局和前端布局对比
-  在flutter中设置布局，需要赋予依赖布局widget，如：container,center,padding等；布局widget和UI widget职责分的很清。在前端中并没有很多布局widget的概念在，任何UI元素都是可以被布局的，只是行内元素和块状元素的区别；
-  缺点：带来页面嵌套层数过多；不是过于灵活和维护。
