---
title: cocos 2d游戏——I wanna save the princess
---
<h2 style="text-align: center;">基于cocos-2dx的游戏制作——I wanna save the princess</h2>

<b>在进行了两周的cocos学习之后，可以开始进行游戏的创作了。
I wanna主要复杂的地方在于地图的设计以及逻辑实现。下面依次进行介绍。（使用c++）</b>

<h3 style="text-align: left">一．	瓦片地图——tile map</h3>
<h4 style="text-align: left">1.	地图整体的大小。</h4>

配合电脑可以全屏显示，设置为1080X1920的大小。
![](https://i.imgur.com/nxXJgh7.png)


<h4 style="text-align: left">2.	图块的大小。</h4>
![](https://i.imgur.com/PIXpNM7.png)
使用Tile map制作地图，因为它非常方便，可以将图片素材直接放到图块中，并且大小可以随意调节。
![](https://i.imgur.com/XM4Csd9.png)



比如：所有的地图图块设置为30X30像素，因此普通的土块和草地都是30X30的大小。
![](https://i.imgur.com/ApNK9MW.png)

但是在下面的场景中，因为水是直接在tile map中显示的，所以设置为了1920X900的大小。
![](https://i.imgur.com/wUayzYq.png)


<h4 style="text-align: left">3.	图层的设置。</h4>

在这个界面中，可以新建多个图层，将不同属性的图块放入。
![](https://i.imgur.com/yWCTAQL.png)

比如：土块和刺是分开的两个图层。
![](https://i.imgur.com/ZdfvPzJ.png)

![](https://i.imgur.com/XNNeWdU.png)
每一个形状的刺分别的一个图层。
向上的刺。
![](https://i.imgur.com/F1SWGPV.png)

向左的刺。
![](https://i.imgur.com/9ExyVbC.png)

隐藏的刺与可以触发的刺也是不同的图层。
地图上直接可见的，向上的刺。
![](https://i.imgur.com/c439TCn.png)
并非直接可见，需要触发条件的，向上的刺。
![](https://i.imgur.com/ADV21xM.png)

在图层的设置中，可以将同一属性的图层用一个新的图层覆盖，并且设置不可穿透的属性，这样在导入图层的时候会比较方便。
![](https://i.imgur.com/P0Z1Y5h.png)
在所有不可穿透的图层中，覆盖了一层红色图层，在vs中导入的同时，设置为不可穿透。
![](https://i.imgur.com/DSlwma2.png)
（不可穿透是利用下文中掩码的作用。）


<h4 style="text-align: left">4.	人物图层。</h4>

在建立图层的时候，选择添加对象层，然后选择建立矩形，在地图上的任一个地方画出任意大小的矩形，代表人物。
![](https://i.imgur.com/tsLqFmW.png)
（相应操作在图上用红色方框表示。）


<h4 style="text-align: left">5.	特殊图层。</h4>

因为I wanna游戏的特殊，经常有不同的隐藏刺。这个部分首先需要在不同的图层中实现，然后需要一个对应的触发图层。

观察红色方框中图层的顺序，现在的位置是游戏地图中正常图层的位置，即土块将隐藏刺遮住了。
![](https://i.imgur.com/2GKSLCB.png)

调整顺序后可以看到隐藏刺。
![](https://i.imgur.com/zQZWbdh.png)

地图中红色图层的作用是，判断人物当前的位置x坐标是否与此图层中的某一个相同，相同则触发刺向上飞的事件。
![](https://i.imgur.com/yf5xcJK.png)

这个触发图层的作用是，在地图中，人物在触碰到这个图层的同时，触发对应tag中的事件，比如让刺飞出，或是在踩到触发图层时冒出。

![](https://i.imgur.com/gGIJNJK.png)
导入的图层为上一张图片中的yincang图层，设置tag为4。
![](https://i.imgur.com/8UA4TaN.png)

人物的tag为1，当两个物体的tag分别为1和4的时候，触发事件。
![](https://i.imgur.com/Tjxnvns.png)

在导入隐藏刺的同时设置冒出的移动，当人物与刺所在的图块接触，刺冒出。
![](https://i.imgur.com/LSQgR0s.png)

触发刺飞出的事件。
![](https://i.imgur.com/cUsSdHQ.png)


<h3 style="text-align: left">二．	物理引擎</h3>
<h4 style="text-align: left">1．	建立物理世界。</h4>
![](https://i.imgur.com/I2FgNHO.png)



<h4 style="text-align: left">2．	重力的添加以及改变。</h4>

添加在创建物理世界时写入。
在第三个场景的水中，需要更改重力的大小。
![](https://i.imgur.com/U22rqfa.png)


<h4 style="text-align: left">3．	添加不同的刚体。</h4>

普通的刚体，是矩形的。
![](https://i.imgur.com/mHgHJV6.png)

因为刺是三角形的，所以需要建立一个数组存储三角形的三个顶点坐标，然后再附给物体，这样就是一个三角形的刚体。
![](https://i.imgur.com/lAvxPE3.png)


<h4 style="text-align: left">4．	介绍三种掩码。</h4>

类别掩码setCategoryBitMask，接触检测掩码setContactTestBitmask，碰撞掩码setCollisionBitmask。
分别将两个物体的类别掩码与接触检测掩码进行逻辑与运算，可以判断是否触发接触事件，类似的，可以判断是否穿透或者碰撞。

人物的三种掩码。
![](https://i.imgur.com/Osfqstw.png)


<h4 style="text-align: left">5．	重新开始。</h4>

将当前场景舍弃，重新生成一个新的场景，进行替换。
![](https://i.imgur.com/X5PN8wP.png)


<h4 style="text-align: left">6．	键盘事件。</h4>

人物可以进行向左前进，向右前进，跳跃这三种动作，在此函数中，按下不同的键实现不同的事件。
![](https://i.imgur.com/HsIWwV6.png)


![](https://i.imgur.com/TUX2A2C.png)

<h4 style="text-align: left">7．	标签的添加。</h4>

在导入图层的时候就分别设置不同的tag，以便于在函数中进行相应的判断。
![](https://i.imgur.com/lSDe7rU.png)

人物与刺碰撞，触发游戏结束的事件，在界面中添加游戏结束的图片，并且取消键盘事件，但可以按R键重新开始。（所有的刺tag都为3）
![](https://i.imgur.com/k7Cmekz.png)

在最后切换场景时，有一个被隐藏了的触发图层，在人物接触到的同时进行tag的比较，从而可以切换场景。
![](https://i.imgur.com/FONa3EU.png)
![](https://i.imgur.com/uuU7qTS.png)
![](https://i.imgur.com/MmH6mhx.png)


<h4 style="text-align: left">8．	计时器函数</h4>

进行场景中物理引擎的手动更新。
![](https://i.imgur.com/lVQVhFL.png)


<h4 style="text-align: left">9．	碰撞检测。</h4>

利用三种掩码进行判断。
人物与土块。（人物的掩码在上方，三个都是7）
![](https://i.imgur.com/dCYH27I.png)
（这个图层就是上方介绍过的覆盖图层）
进行判断后为不可穿透。

人物与水。
![](https://i.imgur.com/VYZNULt.png)
