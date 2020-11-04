# SETASK1

## Analyze the home page loading of [www.sjtu.edu.cn](www.sjtu.edu.cn)
##### 0. 文字解析
   - 输入的网址在通过DNS解析后得到服务器地址
   - 浏览器向服务器发起https请求，经过TCP/IP三次握手确认链接后，服务器将需要的代码发回浏览器。
   - 浏览器接收到html代码后经历以下三个步骤完成网页的加载。
##### 1. DOM构造
   - 浏览器将接收到的html文件解析成一颗树：DOM树
   - 然后将接收到的css代码分别放到对应的DOM树节点上，得到一棵带有样式属性的的DOM树：CSSOM树
##### 2. 布局
   - 浏览器按从上到下，从左到右的顺序遍历CSSOM树的文档节点
   - 计算节点的大小和坐标等属性
##### 3. 绘制画面

## Carry out my optimization solution
1. 直接在浏览器中输入服务器地址。
2. 将服务器架设在与终端更近的地方。
3. 将资源文件与HTML文件放在一起或将资源文件放在访问速度更快、与终端距离更短的服务器上，并将其链接到HTML中。

#### [浏览器解析渲染页面原理](https://www.zhihu.com/question/30218438/answer/84704484)
> 首先，开源浏览器一般以8k每块下载html页面。
然后解析页面生成DOM树，遇到css标签或JS脚本标签就新起线程去下载他们，并继续构建DOM。
下载完后解析CSS为CSS规则树，浏览器结合CSS规则树和DOM树生成Render Tree。
注意：构建CSS Object Model（CSSOM)会阻塞JavaScript的执行。JavaScript的执行也会阻塞DOM的构建。
JavaScript下载后可以通过DOM API修改DOM，通过CSSOM API修改样式作用域Render Tree。
每次修改会造成Render Tree的重新布局和重绘。只要修改DOM或修改了元素的形状或大小，就会触发Reflow，单纯修改元素的颜色只需Repaint一下（调用操作系统Native GUI的API绘制）。![](https://pic2.zhimg.com/e8bc40d7006f13fa0a191d774b7db36a_r.jpg?source=1940ef5c)
(自知乎引用：
作者：陈金
原文：[https://www.zhihu.com/question/30218438/answer/84704484](https://www.zhihu.com/question/30218438/answer/84704484))