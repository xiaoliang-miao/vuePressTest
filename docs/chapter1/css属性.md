### user-select

| **属性值** |                           **说明**                           |
| ---------- | :----------------------------------------------------------: |
| all        | 当所有内容作为一个整体时可以被选择。如果双击或者在上下文上点击子元素，那么被选择的部分将是以该子元素向上回溯的最高祖先元素 |
| auto       |              文本将根据浏览器的默认属性进行选择              |
| contain    |        选择该元素范围内的文本，只支持(Explorer未测试)        |
| none       |                元素和子元素的文本将无法被选中                |
| text       |                        文本可以被选中                        |
| inherit    |                      继承父元素的此属性                      |
| initial    |                     设置为初始的样式属性                     |
| revert     | 样式表中定义的元素属性的默认值。若用户定义样式表中显式设置，则按用户定义的设置否则，按照浏览器默认的的样式设置在否则，等价于unset |
| unset      | 如果该属性可以被继承，则是继承的值，不可以被继承(initial),则是默认的值 |

### backface-visibility

1、`backface-visibility：visible`
默认值，背面朝向用户时**可见**

2、`backface-visibility：hidden`
背面朝向用户时**不可见**。

### clip-path

inset(): 定义一个矩形

```css
//语法
inset( <length-percentage>{1,4} [ round <border-radius> ]? )
//说明
inset()可以传入5个参数，分别对应top,right,bottom,left的裁剪位置,round radius（可选，圆角）

//示例
clip-path: inset(2em 3em 2em 1em round 2em);
```

circle(): 定义一个圆 

```css
//语法
circle( [ <shape-radius> ]? [ at <position> ]? )
//说明
circle()可以传人2个可选参数；
1. 圆的半径，默认元素宽高中短的那个为直径，支持百分比
2. 圆心位置，默认为元素中心点
//示例
clip-path: circle(30% at 150px 120px);
```

ellipse(): 定义一个椭圆

```css
//语法
ellipse( [ <shape-radius>{2} ]? [ at <position> ]? )
//说明
ellipse()可以传人3个可选参数；
1. 椭圆的X轴半径，默认是宽度的一半，支持百分比
2. 椭圆的Y轴半径，默认是高度的一半，支持百分比
3. 椭圆中心位置，默认是元素的中心点

//示例
clip-path: ellipse(45% 30% at 50% 50%);
```

polygon(): 定义一个多边形

```css
//语法
polygon( <fill-rule>? , [ <length-percentage> <length-percentage> ]# )
//说明
<fill-rule>可选，表示填充规则用来确定该多边形的内部。可能的值有nonzero和evenodd,默认值是nonzero
后面的每对参数表示多边形的顶点坐标（X,Y），也就是连接点

//示例
clip-path: polygon(50% 0,100% 50%,0 100%);    
```

==圆形==

```css
<style>
.outer{
  width:100px;
  height: 100px;
  background:orange;
  -webkit-clip-path: circle(50% at 50% 50%)
}  
</style>
<div class="outer"></div>
```

==椭圆==

```css
<style>
.outer{
  width:100px;
  height: 100px;
  background:orange;
  -webkit-clip-path: ellipse(25% 40% at 50% 50%);
}  
</style>
<div class="outer"></div>
```

==矩形==

```css
<style>
.outer{
  width:100px;
  height: 100px;
  background:orange;
  -webkit-clip-path: inset(5% 20% 15% 10%);
}  
</style>
<div class="outer"></div>
```

==三角形== `-webkit-clip-path: polygon(50% 0%, 0% 100%, 100% 100%);`

==菱形== `-webkit-clip-path: polygon(50% 0%, 100% 50%, 50% 100%, 0% 50%);`

==梯形== `-webkit-clip-path: polygon(20% 0%, 80% 0%, 100% 100%, 0% 100%);`

==平行四边形== ` -webkit-clip-path: polygon(25% 0%, 100% 0%, 75% 100%, 0% 100%);`

==五边形== `-webkit-clip-path: polygon(50% 0%, 100% 38%, 82% 100%, 18% 100%, 0% 38%);`

==六边形== `-webkit-clip-path: polygon(50% 0%, 100% 25%, 100% 75%, 50% 100%, 0% 75%, 0% 25%);`

==七边形== `-webkit-clip-path: polygon(50% 0%, 90% 20%, 100% 60%, 75% 100%, 25% 100%, 0% 60%, 10% 20%);`

==八边形== `-webkit-clip-path: polygon(30% 0%, 70% 0%, 100% 30%, 100% 70%, 70% 100%, 30% 100%, 0% 70%, 0% 30%);              `

==左箭头== `-webkit-clip-path: polygon(40% 0%, 40% 20%, 100% 20%, 100% 80%, 40% 80%, 40% 100%, 0% 50%);`

==右箭头== `-webkit-clip-path: polygon(0% 20%, 60% 20%, 60% 0%, 100% 50%, 60% 100%, 60% 80%, 0% 80%);`

==星星== `-webkit-clip-path: polygon(50% 0%, 61% 35%, 98% 35%, 68% 57%, 79% 91%, 50% 70%, 21% 91%, 32% 57%, 2% 35%, 39% 35%);`

==叉号== `-webkit-clip-path: polygon(20% 0%, 0% 20%, 30% 50%, 0% 80%, 20% 100%, 50% 70%, 80% 100%, 100% 80%, 70% 50%, 100% 20%, 80% 0%, 50% 30%);` 

### filter:drop-shadow

drop-shadow():将内部元素投影生成阴影,而非box-shadow生成盒子阴影

用于给不规则盒子添加阴影，，添加阴影的方式针对区域里的像素点，box-shadow是针对盒子做阴影

```html
<style>
    .box{
      width: 200px;
      height: 100px;
      background-color: skyblue;
      margin-top: 200px;
      margin-left: 500px;
    }
    .box::before{
      content: '';
      display: block;
      width: 40px;
      height: 40px;
      background-color: skyblue;
      transform: rotateZ(45deg);
      float: left;
      margin-top: 30px;
      margin-left: -20px;
    }

    .box2{
      width: 200px;
      height: 200px;
      background-color: red;
      clip-path: polygon(0 50px,50px 0,150px 0,200px 50px,200px 150px,150px 200px,50px 200px,0 150px);
      /* box-shadow: 0 0 2px 2px yellow; */
    }
    .father{
      filter: drop-shadow(0 0 5px yellow);
    }
  </style>
</head>
<body>
  <div class="box"></div>

  <div class="father">
    <div class="box2"></div>
  </div>
</body>
```

