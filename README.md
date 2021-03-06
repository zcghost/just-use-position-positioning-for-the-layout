# just-use-position-positioning-for-the-layout
# 恰用postion定位进行布局
![](http://i.imgur.com/Md3OSmu.jpg)

前言：

在我们进行网页设计时，首先应该是拿到UI美美甩过来的psd文档或者png图片，然后自己大刀阔斧，一股劲先切图后编码，曾今我也有过信心满满，自我感觉良好，不已为然。然而就在后台工程师套页面时，进行了某些局部性的手术，却一切都变了！！原本是一张的堪称完美的页面，此时，却变得四肢不全，胳膊与腿，脑袋跟屁股，全错乱了，不得不令人失落和懊恼，于是便是各种返工和bug修复，尽管一定程度上修修补补，改来改去，能把问题给解决，但是此时，人都已经废一半了的，冗余繁重一些不必要的代码，code健壮性可想而知，甚至有时改着改着面目全非，混乱不坎，草草了事，不仅耗时费脑，还心生凝问，自信心瞬间被打击得落一地了的，产生这一系列的原因，追本溯源，其实就是自己页面布局的问题，前期的准备和战略因素没有规划好。在我看来，一个好的作品一定是即使在去掉它美丽的外表下，面容依旧玉树临风，昂然挺立的，一位好的军师一定是拥有未雨绸缪，排兵布阵，越众人之上的。言归正传，今天，我就对自己的学习，聊聊心得，希望对你有所帮助，本人水平知识有限，如果你是大神，可以直接略过哈O(∩_∩)O 

`正文从这里开始~`

前面一文，《从小小标签元素到绚目多彩的网页》中比较唠叨的谈到了关于浮动这一话题，没错，这东西确实比较繁琐，它既充满了神奇又时常令人懊恼，暴露出了种种的诟病，在使用它的同时，稍有不慎，往往会导致一些意料之外的结果，令人痛苦不已，明明是就是这样的，但是就是不能依我所意，于是我试试margin,试试positon,等等的，用得凌乱不已，往往在使用后，还不能忘记给它"擦屁股"(清除浮动)的痛苦，否则，后面便是怎么搞都是不爽，所以很有必要重视它的学习的，如有不知，请翻阅上文8大奇淫绝技如何进行清除浮动。其实，定位(position)的技术毫无凝问,它的地位是无法撼动的，当我们在pc电脑浏览某些网站时，猛的一打开，便弹出一个遮罩层，一讨厌的广告，某些网站还时不时弹出一些来来回回的广告，对话窗口，桌面上猛地弹出个一MM，手一哆嗦，不慎点击，于是便强行把你拉住某某房间，结果你懂的，流氓得不行，当然这只是一方面了，定位是无处不在的，看下面一张图以京东为例：
![](http://i.imgur.com/uoBJSDu.png)

一般常常用到定位的：比如上图的：下拉二级菜单，二级导航，轮播无缝切换，下面左侧的楼梯式导航，右侧的固定列表，及置顶按钮等等的。凡是页面上可动移动，可拖拽的，可覆盖在其他页面元素之上显示的，其实都用了定位
> 如何能够改变一个元素在页面中的位置

方法1：float:浮动（left/right）

方法2：margin(top,right,bottom,left)

方法3：利用定位position

方法四：利用js对元素进行DOM动态的操作(其实也是要么改变margin值或者添加position：更改top,right,bottom,left)
其中方法3:是用的比较频繁的：
包含块的概念：官方解释为最近的块级祖先元素，通俗得来讲，就是子元素离他父级最近的元素，这个概念很重要，关于框(box)的很多定位尺寸的计算都和这个矩形边界有关，它是一个相对的概念，一个元素的父元素，通常就是这个元素以及子孙元素的包含块，元素是被包的关系（比如后期常常用js做的拖拽，等等的，获取元素自身的一些属性进行计算时，要做相关的交互效果时，往往这个概念就发挥作用了的）这就好比：小时候，你向长辈们要钱买东西吃时，首先你找你爸妈要钱，爸妈若不在，便找爷爷要钱，反正是找离最近的人了。那么想改变一个元素的位置，是通过哪些手段来的呢？先了解下`偏移属性(offset)`这个概念
理解这个东西，我觉得是很重要的。

`top`  `right` `bottom` `left`

值：`length(具体数值)`  |  `percentage(百分比)` | `auto(自动)` | `inherit(继承)`

初始值:auto

应用于：只有定位的元素才拥有这些属性（也就是position排除static）
百分数：对于top(上)和bottom(下)，相当于包含块的高度，对于left(左)，right(右)相当于包含块的宽度

计算值：对于static元素为auto,对于它的长度值，是相应的绝对长度，对于百分数值，则为指定的值，否则是auto的

觉得最为重要的offset(偏移)：距离包含块(注意这个包含块是相对位置的，要看把谁作为参考物)最近的偏移，当我们刚开始学它的时候，总是不明觉易，往往对它不求甚解，嗨，这东西确实好用，脑子一股热的，管他三七二十八的呢，浮动和margin解决不了的问题，就用position定位偏移的，然而当发现使用它时，如一步走错，却步步走错的，由于过多的不明确使用定位，表面上看起来，没有任何问题，但是如果要进行二次拓展或者等待后台，给你进行手术整形时，往往问题就很大了，相信遇到的朋友，是身有体会的，当然深度的理解对后面js处理元素计算位置时，是很有帮助的，比如说：js中获取一个元素自身宽高度(元素.offsetWidth/Height)(注意这个宽高度，是包含了自身设置的width+padding+border的不包括margin,可以自行测试一下的)，获取距离浏览器上下可视区域位置(元素.offsetLeft 元素.offsetTop，注意是包含margin值的，`注意这原生的方法，当元素不存在或者隐藏时，是获取不到该值的，这与jquery是有很大的差异，如果不注意，在使用原生时，做些效果时，就会令自己找不着背，丈二和尚摸不着头脑的)`，整个文档的宽高度(document.documentElemento.clientHeight/clientWidth).要是有滚动高度的话，还得加上scrollTop(),以及jquery中的width().height(),innerWIdth/height,outerWIdth()/height(),以及对象.offset().left,对象.offset().top，元素位置等等的，仔细想想，如果这些偏移量和盒模型的一些参数没有彻底的弄明白，在后面的js做一些关于物体运动的效果，动态的获取元素位置等等，无论是js还是用Jquery，试来试去，用得是相当混乱的，一旦遇到此类似的问题，犹如蜂蜜般蛰得你疼痛不已的，如此相关的问题，以后在js中详谈，还是比较喜欢图解，边看图，边理解更:
![](http://i.imgur.com/wz3gKSL.jpg)

根据上面的图解和代码示例的，仔细体会top,right,bottom,left了，下面用文字稍稍解释下：

`top`:描述定位元素上外边距边界离其包含块(父元素，注意，当absolute没有设置相对定位时，它会不断的往上找，默认是：相对元素是body,html，所以有时候在做某个遮罩层的时候，发现只盖住某一局部，并不能遮罩整个文档令自己非常懊恼，这就是定位元素出了问题，一般解决的办法是：要么固定定位，body,html，把宽高设置为100%的，即可解决),当top值为正，会把定位元素的上外边距向下移，否则，上移(记住：下正，上负即可)

`left`:描述定位元素的左外边距边界在其包含块左边界右边(正值)或左边(负值)，值有多大，就滚多远，若是正值，则会把定位元素的外边距边距移到包含块的右边，否则，移到包含块的左边(正右，父左)

`bottom`:同理可理解（下移正，上移负）

`right`:同理可理解（左移正，右移负）
> 横扫position进行排兵布阵

position值：`static` |`relative` | `absolute` | `fixed` | `inhert`
初始值：`static`

继承性：无

position:static 默认状态就是static，若在css中为元素定义top,right,bottom,left,z-index,都不会生效，换句话说，就是如果你想设置元素的偏移量和z-index:那么就必须为元素定义position的属性，static除外，注意在所有的定位(position)默认是static,什么都不写就是相对定位，而使用position:relative，如不设置top,left.z-index:等值的情况下，就和默认static表现一样

position:relative;相对定位

特点：
1. 不会影响元素本身特性（块级元素与行间元素）
2. 不会使元素脱离文档流，仍然是占位置的
3. 如果没有定位的偏移量(top,right,bottom left),对元素本身没有任何影
响          
4. 一般都会配合绝对定位进行使用
> 关于IE6下父元素包不住子元素的问题

当子元素的高度设置为相对定位时，又加上它自身的高度比它父级元素要高时，那么在低版本万恶的ie6浏览器下，即使父元素用了overflow:hidden;也包不住子元素，会溢出的情况:如下图所示
![](http://i.imgur.com/KoEiVew.png)

解决办法：父元素跟子元素一样，加上相对定位(position:relative)或者加上绝对定位，即可
postition:absolute;

特点：

1. 定位的元素会脱离文档流，不占据位置空间，类似浮动后的效果，拥有浮动的一些基本特性，比如下面的2，在不设置内容的时候，由内容撑开，提升了层半级。
2. 使内嵌元素(也就是行内元素,比如span，i标签之类的)，支持宽高的(所以有时候，如果给一个行间元素设置了绝对定位，就没必要后面还要加一行display:inline-block了的，相当于是它的升级版，既解决了ie67不能横向显示的问题，又拥有绝对定位的特性，注意，换行会被浏览器解析，要么加浮动，要么去掉代码间隙即可解决)
3. 在不定义z-index的情况下，absolute元素会优先于其他元素之上，将其他元素给覆盖掉
4. 块属元素标签内容撑开宽度,值得注意的是：`在使用绝对定位时，若不指定父元素的position(注意这个定位，不一定父元素非得就是relative还可以是fixed固定定位，绝对定位，当然排除static),absolute将相对于整个html文档进行绝对定位`，见下图分析:

![](http://i.imgur.com/8HVEKdT.jpg)

从上图分析可得：使用绝对定位元素，不一定要使用相对定位(position:relative),曾今我有一段时间也曾混淆过，始终觉得使用绝对定位，就得使用相对定位的，然而却不是这样的，只要它的包含块是定位属性，就可以了的，当然一般使用相对定位时，绝大部分都是配合绝对定位进行使用，具体的情况还是具体分析咯

> 关于在IE6低版本下使用绝对定位1像素偏差的问题

原因：当父级元素给定的宽高是个奇数时，在IE6低版本下right,和bottom会有一像素的偏差：

解决办法：在设计时，宽高尽量使用偶数
![](http://i.imgur.com/FwFZJnt.jpg)
`positon:fixed`;固定定位

特点：

1. 与绝对定位比较类似，但是却又不同于它，它是相对于浏览器的窗口进行定位的，也就是说，无论网页如何滚动，该元素始终停留在屏幕上的某个位置上，“永久性”的，比如最上面的京东右侧的侧边栏，始终都是固定在右侧，对用户可见的，底下的置顶操作等等，都是使用position:fixed进行定位的
2. 元素会完全从文档流中去除，不会有相对问文档任何部分的位置（比较特例独行，只听命于浏览器窗口）

> 关于position:fixed在IE8以下浏览器是不兼容的

在低版本浏览器下position:fixed是不兼容的，那么也可以用绝对定位模拟出固定定位，其实也就是用js进行控制，用css hack的方法，但是一般都很少用，列在这里，无非就是有时候，面试的时候，有的人问你对css hack有多少了解的，出现css hack的原因是，同一段代码在不同的版本的浏览器里显示的效果差强人意，不尽相同，所以就出现了hack技术，真正开发的时候，鬼才用的，针对IE6：属性前加上_  IE7属性前:加上* 号，比如:_height:100px;*height:100px;等等的，这里仅仅列一下在IE6下兼容性代码，可以测试，在样式里面

.fixed{
      width:XXpx;
      height:XXpx;
      top:0x;
      _position:absolute;
      _top:expression(eval(document.documentElement.scrollTop)；
      position:fixed; // 高版本的代码写在最后后面
})

> 扯扯z-index的使用
z-index

值：具体数值 | `auto` | `inhert`

初始值：auto

应用范围：只针对定位元素，排除static

继承性：无

注意：使用z-index:一定是用于定位元素的（不管是相对定位，还是绝对定位，固定定位），利用z-index可以改变层级关系，也就是通俗的来讲改变定位元素之间的相互覆盖顺序,当在同一层级下，后面的数值越大，它的权值就越大，在使用它的时候,我觉得要慎用，并不是定位元素就得使用z-index的，得分清具体情况,不要滥用z-index的,否则的话，当页面在结构比较复杂，层层嵌套，并列的情况下，z-index使用的过多，不当，就会出问题，js操作DOM做某些操作时，就会出意料之外的结果，取决于用不用z-index，看具体的页面结构和需求，而对于后面的数值，并不是越大就越好，每当使用时，来个999999的，这样没有多大意义，当使用得多时，自己也会混乱，搬起石头砸自己的脚啊，只要想同级的定位元素，一个元素想要覆盖在另一元素之上，那么覆盖层的元素层级稍比它大即可。
下面分别用定位写两个实例来热热脑的，毕竟，说得在多，讲得在好，理论终究是理论，实战才是检验真理的唯一标准啊

`示例1：`
/*
1. 绝对定位和相对定位
2. 利用了一冒泡机制，实现了一个侧边栏鼠标移入的显示和隐藏（
有时候，利用冒泡一些方法不仅减少很多代码，特别是后面的事件委托，对做一些动态的dom操作，好处就是：在性能上相比较比较好，减少了dom元素的操作，对后续动态添加的元素是有直接操作行为的。委托的事件添加在父元素或者祖先节点上，但是触发事件的行为却添加在子元素上
3. 事件冒泡：单击首先发生在目标元素上，然后逐层的向上冒泡，直至docuemnt对象（从下往上的一种方式

![](http://i.imgur.com/udoBqQB.jpg)
比较弱的实例，主要是平时冒泡用得少，自己要多尝试着换种思路写的，而后面的js事件委托也是相当的重要，利用的也是冒泡的机制，面试时，也是经常问问这方面的问题的，所以稍稍提了一下，关于事件操作，以后在聊
`示例2：`
`置顶的操作`
![](http://i.imgur.com/jIFkW8C.jpg)

好了，一个简单的置顶操作就完成了的，当然平时一直都习惯了用jquery写，在加上一点缓冲动画的，就更加完美了的，这里简单的用原生js实现了，搞点动画，有些麻烦的，写的过程中，发现定义变量的时候，就是如上图代码中，window.onscroll上面的两行代码，发现若定义在全局坏境里，却是有问题的，卡了一下，想想应该是作用域的问题，关于闭包和作用域，经常性把自己整晕的，我还是得滚回去多看看这方面的东西的，不在这瞎掺和了的
好了，总结一下的吧，其实关于浮动和定位是css中两个非常重要的东西，非常"耐人寻味":-(的，不仅麻烦而且还B事多，如果使用一不小心，就令自己有时很迷惑，对于如何使用浮动，和使用浮动的应用场景，及时的清除浮动，和对元素进行定位时，元素的重叠，叠放顺序，大小，放置等等的都需要小心的考虑，除此之外，还必须考虑浮动元素和定位元素与正常流的关系，因此在布局，排兵布阵时，就得有所顾忌，所谓错走一棋，满盘皆输，有这么一点意思咯

`以下是本篇提点概要`
1. 页面中的定位用在哪些地方的
2. 如何能改变一个元素在页面中的位置
3. 理解偏移属性top right bottom left(个人觉得挺重要的)
4. 横扫position进行排兵布阵
5. positio:static | relative | absolute | fixed
6. 扯扯z-index的使用
7. 利用冒泡，绝对定位，相对定位写了一鼠标显示隐藏的侧边栏分享的小示例，利用固定定位position:fixed写了一个置顶的操作

内容不多，但是略有些杂，总的来说，浮动和定位还是挺重要的，如何排兵布阵，完成一个完美的布局和实现炫目多彩的网页效果完全足够了的

![](http://i.imgur.com/nA2SCCw.jpg)

`更多精彩内容，敬请关注微信itclan公众号`
