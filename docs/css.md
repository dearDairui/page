# CSS 整理

---

css 的整理，主要是对《css 揭秘》这本书的阅读的总结

## 1. WEB 标准与编码技巧

### 1.W3C 的组成

W3C 并不生产规则，他将技术规范整合到一起，其组成结构为：

1. 86 位来自 W3C 的会员公司的成员
2. 7 名特邀专家
3. 5 名 W3C 的工作人员

每项规范初始到成熟会经历下边几个步骤：

1. ED：编辑草案，初始阶段，部分可能不会被接受
2. FPWD：首个公开发布版本，接收工作组的公开反馈
3. WD：工作草案接收社区，工作组的反馈，浏览器开始实现
4. CR：候选推荐规范，这个时间浏览器开始实现测试
5. PR：提名推荐规范，会员公司最后的修改机会，一般不会修改
6. REC：正式推荐规范，一项技术规范的形成

### 2.CSS 历史

CSS 1 规范在 1996 年产生，内容较少在一个网页就可以写下，用 A4 打印也就 68 页

CSS 2 规范在 1998 年产生，定义更加严格，同时添加了更多的功能，这个时候就更多了，480 页 A4，这时候就不能记忆了

css 2 以后发现 css 变得越来庞大，于是开始将他们打散到各个模块中去，每个模块单独成为一个版本，那些延续了 css 2 的已有的特性的直接升级到 3 这个版本。如果是新加的功能模块，则版本号为 1。比如 css 的变形 flex 网格布局等。

#### 2.1 浏览器前缀：

> 自相矛盾的，永不可能执行的悖论,浏览器的前缀因已是一场史诗般的失败！

每个浏览器都有可实现那些实验性的（甚至是私有的，非标准的）特征，只要在属性前边加上一个前缀，就区别了不同浏览器的实现，但是这种问题就会产生滥用前缀的问题，开发者都开始有意识的给每个属性都去加上前缀，下边代码就出现了：

```css
-moz-border-radius: 10px;
-ms-border-radius: 10px;
-webkit-border-radius: 10px;
-o-border-radius: 10px;
border-radius: 10px;
```

其实上边的 css 代码中 -ms-border-raduis 和 -o-border-raduis 一开始这两家浏览器都支持 border-raduis，但是开发者还是会写上，毕竟我们很难记住哪些浏览器实现了哪一种属性。现在唯一的好消息是浏览器厂商开始不这样实现这些实验性的属性了，他们在浏览器中加入了配置开关，但是这种影响还会持续很长时间的

使用自动添加前缀的脚本：

1. CSS3 的 Please , pleeease
2. Autoprefix
3. -prefix-free (http://leaverou.github.io/prefixfree)

### 3.编码技巧

#### 3.1 尽量减少代码复用

> DRY (do not repeat yourself) , 尽量减少改动时要编辑的地方！

1. 代码易于维护 vs 代码量少 ：有时候并不能都满足
2. currentColor:css 第一个变量 ，他和当前元素的文字颜色保持一致
3. inherit：绑定父元素的计算值

## 2.背景和边框

### 2.1 半透明边框

书中的这个已经不适合最新的 chrome 了，被修复了？

### 2.2 多重边框

1. box-shadow 方案
   只能够实现实线边框，不能实现虚线的边框
2. outline 方案
   只是适用于两层的边框；边框不会贴合 border-radius,这个可能是个 bug；

### 2.3 灵活的背景定位

1. background-position 的扩展语法方案

在 css 第三版的背景与边框中 background-position 得到了扩展，它允许我们做随意的扩展 可以指定背景图片的距离任意角的距离：

```css
/**
 * Flexible background positioning
 * via extended background-position
 * 代码来源于 http://dabblet.com/gist/0f226e63595d1bef88cb
 */

div {
    background: url(图片) no-repeat
        bottom right #58a; /*这里的代码是为了版本回退的，如果不支持position的还是会默认到右边的底部位置*/
    background-position: right 20px bottom 10px;
    /* Styling */
    max-width: 10em;
    min-height: 5em;
    padding: 10px;
    color: white;
    font: 100%/1 sans-serif;
}
```

最终实现的效果为：距离底部 10px 右边 20px ;

![blockchain](5.png "http请求")

但是这种方案如果改动了 padding 值，最终我们还要改动 background-position 的值，这样就很烦

2. backgdound-origin 方案
   我们要实现的是背景自动跟着我们的内边距走，每个元素都有三个矩形框，分别是 border-box content-box padding-box ,在默认的情况下 background 是以 padding-box 为准的，不过我们可以使用 background-origin 来改变这种现象：

```css
background: url(图片) no-repeat bottom
    right #58a;
background-origin: content-box;
```

3. calc( ) 计算方案

```css
background: url(图片) no-repeat bottom
    right #58a;
background-position: calc(100% - 20px) calc(100% - 10px);
```
