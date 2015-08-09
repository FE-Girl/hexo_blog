title: 有关inline-block
date: 2014-06-07 16:41:41
tags: inline-block
---

display的三个常用值
======

- display:block;   将元素显示为块级元素。其高度、行高以及顶和底边距都可控制。宽度缺省是它的容器的100%，除非设定一个宽度。
- display:inline;   将元素显示为行内元素。和其他元素都在一行上，高、行高以及顶和底边距不可设置。宽度就是它的文字或图片的宽度，不可改变。
- display:inline-block;    格式化为行内元素的块容器。将对象呈递为内联对象，但是对象的内容作为块对象呈递。旁边的内联对象会被呈递在同一行内，允许空格。准确来说，应用此特性的元素呈现为内联对象，但可以设置高度和宽度等块级元素属性。注意在设置margin:0 auto;时没效果，因为它呈现的是内联对象，占据的不是一整行。

inline-block
=========
>浏览器兼容问题：
  - IE从5.5就开始支持display:inline-block;，只是支持的并不是那么的完善；
  - IE6中inline元素只要触发了haslayout其表现就类似于inline-block
  - IE6中block元素即使触发了haslayout也不能具有inline-block元素不换行的特性，必须先将其强制转换为inline元素，再触发haslayout

>>兼容各浏览器的写法：
    ` display:inline-block;     //现代浏览器 和 IE6、7 的inline元素`
    ` *display:inline;     //IE6、7 block元素`
    ` *zoom:1;        //IE6、7 触发layout`

>>解决IE6、7 block元素表现为inline-block还有一种方法：
    ` .content {`
    `       display:inline-block;   //先触发其layout`
    `  }`
    ` .content {`
    `       *display:inline;     //再强制转换成inline元素`
    `  }`

>间隙问题
  - display设置为inline和inline-block的元素前后会有间隙（不是固定大小的），但在IE6、7中block的元素设置inline-block后没有间隙。
  - 产生间隙的根本原因：HTML中的换行符、空格符、制表符等产生了空白符，而这些归根结底都是字符，那么它们的大小都是受font-size来控制的。
  - 解决间隙的方法：
    `  font-size:0;   //所有浏览器`
    `  letter-spacing:-5px;     //safair等不支持字体为0的浏览器`
    `  *letter-spacing:normal;`
    `  word-spacing:-1px;    //IE6、7`
      

- 上述所有操作都是在父元素设置的，那么子元素都会继承这些属性，字体大小为0了，子元素就什么都看不到了，这并不是我们想要的。 同时字符和单词间距我们也要把它重置为默认值。font-size: 12px; letter-spacing: normal; word-spacing: normal;