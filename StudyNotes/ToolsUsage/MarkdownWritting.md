今天（2022/8/3）在学习OpenCV的时候，想到了三个问题，想记录一下。于是想到用现在非常流行的MarkDown文件书写，遇到了一些问题，现已解决，做此纪录。

## 期望
1. 在VS项目中，通过VS的项目管理，创建.md文件，而不是手动在项目文件夹里创建。因为我想让.md文件也被VS项目管理工具管理，可以让它在 **解决方案资源管理器** 中被看见，直接在VS编辑界面编辑，也可以用VS中的Github工具将它 **同步到云端** 。
2. 在VS中编辑.md文件，必须要有预览功能，我做笔记经常截图，所以插入图片的操作必须要方便。

## 结果
1. 期望全部实现

## 操作过程
2. 在VS中创建.md文件，解决资源管理器，项目作用于下->右键->添加->新建项
![](https://raw.githubusercontent.com/ZhangJiaJie955/FigureBed/main/img/20220805172554.png)

添加新的.md文件
![](https://raw.githubusercontent.com/ZhangJiaJie955/FigureBed/main/img/20220805172710.png)

由于安装了VS　markdown的extension，在创建了.md文件后，自动跳到.md文件编辑模式，左边是编辑区，右边是预览区
![](https://raw.githubusercontent.com/ZhangJiaJie955/FigureBed/main/img/20220805173053.png)

编辑好.md文件后，可以直接在 **团队资源管理器** 中看到更改

![](https://raw.githubusercontent.com/ZhangJiaJie955/FigureBed/main/img/20220805173247.png)

并将它push到GitHub远程仓库中：
![](https://raw.githubusercontent.com/ZhangJiaJie955/FigureBed/main/img/20220805173438.png)
同步成功：
![](https://raw.githubusercontent.com/ZhangJiaJie955/FigureBed/main/img/20220805173459.png)
看看GitHub远程仓库的改变：
有了文件
![](https://raw.githubusercontent.com/ZhangJiaJie955/FigureBed/main/img/20220805173600.png)
成功！：
![](https://raw.githubusercontent.com/ZhangJiaJie955/FigureBed/main/img/20220805173622.png)

图片的插入使用PicGo这个开源的小软件
每次截图后，用它把截图上传到GitHub图床仓库，这可以不管在哪儿下载.md文件，这些图片都可以被看见（这就与markdown操蛋的图片插入有关了）

小截个图
![](https://raw.githubusercontent.com/ZhangJiaJie955/FigureBed/main/img/20220805174604.png)

点击 **剪贴板图片** 直接就将截的图上传到了GitHub

![](https://raw.githubusercontent.com/ZhangJiaJie955/FigureBed/main/img/20220805174723.png)

到GitHub提前设置好的仓库中看看：
![](https://raw.githubusercontent.com/ZhangJiaJie955/FigureBed/main/img/20220805174948.png)
图片是在的，

markdown编辑器预览中也有这个图片：
![](https://raw.githubusercontent.com/ZhangJiaJie955/FigureBed/main/img/20220805175034.png )

而且不管在那里打开这个md都会有这张图片，但是要开VPN，因为图片存在GitHub中，不开VPN加载图片很慢。

成功！

## 如何实现的 

1. 在VS项目中添加.md文件很简单，我本想像创建cpp文件那样，点击新建项之后会出现系统自带的选项的，但是没有，但是自己创建  xxx.md文件的效果也是一样的。
2. 添加后的.md文件也被项目git管理，而且之前我也配置好了VS的git相关功能，所以在编辑完成后将他push到远程仓库也很简单。
3. 在VS中编辑.md文件，实现.md文件的预览功能，只需要下个插件就行
 ![](https://raw.githubusercontent.com/ZhangJiaJie955/FigureBed/main/img/20220805180634.png)
操作过程在这里https://blog.csdn.net/qq_35504602/article/details/108054416
4. 最麻烦的就是.md文件中的图片该如何插入。
   众所周知，.md文件插入图片的语法非常麻烦， \!\[]()，我做笔记截图的频率又特别高
   如果不用第三方工具，我用的QQ截图，每次截图后，得首先打开一个聊天框容纳我截的图，再点击另存为才保存到本地然后用markdown语法，复制图片链接到 （""）里面，这样做不仅很麻烦，而且图片保存在本地，当我将.md文件push到GitHub上以后，就看不见这些图片了，如果别人git clone我的notes到他自己的计算机中，就更看不到图片了。

   所以我想用更优雅的方法插入.md文件的图片。

   https://blog.csdn.net/dgut_guangdian/article/details/107245592

   使用GitHub + PicGo解决，具体思路是，在GitHub中创建一个只用来存放图片的repo（专业名词叫图床）,把notes中的每张图片都存在这个repo中，在markdown文件中插入图片的url，而不是本地链接，这样不管在哪里打开这个.md文件，只要连的上GitHub，就可以看到这张图片。而将图片上传至GitHub repo并获取图片的url，就用到PicGo这个开源小软件，配置好以后，可以通过上面的操作流程看出，整个过程非常的方便。

   具体的配置操作可以看上面的链接，这里我主要说明两个问题，这也是我在配置过程中卡壳的地方。
    1. PicGo下载地址 https://github.com/Molunerfinn/PicGo/releases/tag/v2.3.0 拉到最下面的 Assets，
        因为上面博客给的链接一进去是PicGo的GitHub主页，我觉得挺难找的，不过我写这篇文章的时候又找了一遍，发现也还挺好找，😂，可能是我的问题。
    2. PicGo下载好之后的配置，我觉得博客还有官方文档都没说清楚。
   ![](https://raw.githubusercontent.com/ZhangJiaJie955/FigureBed/main/img/20220805210041.png)
   图床的这些配置 **仓库名**，**分支名**，**存储路径**，都指的是远程仓库的东西，我当时就纠结，GitHub有本地仓库和远程仓库，为啥这儿只配置一个仓库的东西？后来想通了，可能PicGo只对remote repo操作，根本不会设置local repo，这样当然也是OK的。

   * **仓库名** 就是在GitHub上创建好repo之后的这个。
   
     ![](https://raw.githubusercontent.com/ZhangJiaJie955/FigureBed/main/img/20220805211152.png)
   * **分支名** 就是main，remote repo的主分支默认是main，还有tm说是master的，给你一个大逼兜。
   * **指定存储路径** 不是在本地哪个文件夹中存这些图片，而是在remote repo，这个 *FigureBed* 中哪个文件夹存这些图片，如果不写的话，点进去 *FigureBed* 就是，如果像图中这样写，*FirgureBed/img* 才是。
    ![](https://raw.githubusercontent.com/ZhangJiaJie955/FigureBed/main/img/20220805211542.png)
    ![](https://raw.githubusercontent.com/ZhangJiaJie955/FigureBed/main/img/20220805211628.png)
   * **自定义域名** 这是修改上传图片后，返回的\!\[]\(url)其中的url地址的， 除非你不能翻墙，需要搞什么cdn加速，否则就不需要写这个东西。
   
       我一开始想的是，图片不都存在这里嘛
       ![](https://raw.githubusercontent.com/ZhangJiaJie955/FigureBed/main/img/20220805212039.png)
       我把这个url设置为自定义域名，到时候它自动在后面加上图片文件名不就ok了。
       
       但是疯狂报错，图片成功上传的，但是返回的markdown命令显示不出图片，我就很烦，卡了半天，然后看视频有的人没有写这个东西也玩儿的挺好，我就索性也不写它，但还是不行，我看别人写这个东西的会有个cdn加速，我就想可能得翻墙，然后VPN一连，才好。。。tmd大坑，卡了半天。

    * 为什么那个url加上图片名称，不能当作图片的url，因为它本来就不是，这他妈也是一个大坑，GitHub上存的图片，这个![](https://raw.githubusercontent.com/ZhangJiaJie955/FigureBed/main/img/20220805213702.png)不是tm的图片url，这只是个网页。这个![](https://raw.githubusercontent.com/ZhangJiaJie955/FigureBed/main/img/20220805215909.png)才他妈是！！！，只有这个url在markdown中才会有图片显示。
        



## 问题
之前遇到过VS编码和GitHub编码不匹配，导致上传GitHub后中文乱码的，但是现在咋没有了。。。。
很神奇，但是还查了这个解决方法。
https://blog.csdn.net/Love_Point/article/details/105658241?spm=1001.2101.3001.6650.1&utm_medium=distribute.pc_relevant.none-task-blog-2%7Edefault%7ECTRLIST%7Edefault-1-105658241-blog-105750175.pc_relevant_default&depth_1-utm_source=distribute.pc_relevant.none-task-blog-2%7Edefault%7ECTRLIST%7Edefault-1-105658241-blog-105750175.pc_relevant_default&utm_relevant_index=2





vscode + Markdown All In One(a vsc extension) + PicGo + Github

自己在文件夹中创建 **title.md** 文件