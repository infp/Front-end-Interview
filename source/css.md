
### HTML 相关问题

#### 1、doctype（文档类型）的作用是什么？

声明页面文档的类型，以及告诉浏览器应该使用哪种模式进行渲染。

#### 2、浏览器标准模式和怪异模式之间的区别是什么？

由于历史的原因，各个浏览器在对页面的渲染上存在差异，甚至同一浏览器在不同版本中，对页面的渲染也不同。在 W3C 标准出台以前，浏览器在对页面的渲染上 没有统一规范，产生了差异（Quirks mode）；由于 W3C 标准的推出，浏览器渲染页面有了统一的标准（Standars mode），这就是二者最简单的区别。总而言之，怪异模式是为了兼容在标准推出之前出现的页面而设置的。

浏览器会根据 doctype 来决定使用哪种渲染模式，比如 `<!doctype html>` 将会触发标准模式。如果页面中没有声明 doctype，浏览器则会使用怪异模式。

#### 3、使用 XHTML 的局限有哪些？ 如果页面使用 `application/xhtml+xml` 会有什么问题吗？

#### 4、如果网页内容需要支持多语言，你会怎么做？在设计和开发多语言网站时，有哪些问题你必须要考虑？

#### 5、`data-` 属性的作用是什么？

当没有合适的属性和元素时，自定义的 `data-` 属性是能够存储页面或 App 的私有的自定义数据。

> Custom data attributes are intended to store custom data private to the page or application, for which there are no more appropriate attributes or elements.

可以通过 `ele.dataset.xxx` 来访问 `data-xxx=""`。

#### 6、请描述一下 cookies，sessionStorage 和 localStorage 的区别？

##### Cookie

1. 每个域名存储量比较小（各浏览器不同，大致 4K）
2. 所有域名的存储量有限制（各浏览器不同，大致 4K）
3. 有个数限制（各浏览器不同）
4. 会随请求发送到服务器

##### localStorage

1. 永久存储
2. 单个域名存储量比较大（推荐 5MB，各浏览器不同）
3. 总体数量无限制

##### sessionStorage

1. 只在 Session 内有效
2. 存储量更大（推荐没有限制，但是实际上各浏览器也不同）

#### 7、请描述一下 GET 和 POST 的区别？

1. GET 将参数放在 URL 的 Query String 里，有长度限制，只支持 ASCII 数据
2. POST 将参数放在 HTTP body 中

另外，HTTP 除了这两种请求方式，还有 HEAD、PUT、DELETE、OPTIONS、CONNECT、PATCH。

相关的话题就是 RESTful 接口，可以看看阮一峰的文章：[《理解RESTful架构》](http://www.ruanyifeng.com/blog/2011/09/restful.html)和[《RESTful API 设计指南》](http://www.ruanyifeng.com/blog/2014/05/restful_api.html)。


### CSS 相关问题

#### 1、描述下 CSS reset 文件的作用和使用它的好处。

CSS reset（CSS 重置），可以重置浏览器对于 HTML 元素的默认样式，作用是让各个浏览器的 CSS 的样式有一个统一的基准。

比较流行的 CSS reset 有Eric Meyer’s Reset CSS、Normalize.css、YUI Reset 等等，进一步可以看 [CSS Reset](http://www.cssreset.com/)。

#### 2、解释下浮动和它的工作原理。

#### 3、列举不同的清除浮动的技巧，并指出它们各自适用的使用场景。

参考：http://stackoverflow.com/questions/211383/which-method-of-clearfix-is-best

#### 4、解释下 CSS sprites，以及你要如何在页面或网站中使用它。

将一些小图片整合到一张大图里面，来达到减少 HTTP 请求的目的。一般我会把单页需要的 icon 整合到一张，整站需要的整合到一张。这样尽量避免加载当前页不需要的图片。还可以把色值相近的图片放一起，可以让压缩的图片体积更小。

在网站中使用 SVG 或 Icon Font 也不错。

#### 5、你最喜欢的图片替换方法是什么，你如何选择使用。

Image Replacement 是说用图片把文字替换掉的技术，常用在标题上。

```html
<h1 class="nir">[content]</h1>
```

```css
.nir {
   height: 100px;	/* height of replacement image */
   width: 400px;	/* width of replacement image */
   overflow: hidden;
}

.nir:before {
   content: url(image.gif);
   display: inline-block;
   font-size: 0;
   line-height: 0;
}
```

参考：http://nicolasgallagher.com/css-image-replacement-with-pseudo-elements/

#### 6、讨论 CSS hacks，条件引用或者其他。

#### 7、如何为有功能限制的浏览器提供网页？你会使用哪些技术和处理方法？

这里有两种思路，一个是渐进增强，一个优雅降级。

1. 渐进增强的思路就是提供一个可用的原型，后来再为高级浏览器提供优化。
2. 优雅降级的思路是根据高级浏览器提供一个版本，然后有功能限制的浏览器只需要一个刚好能用的版本。

当然，工作中的标准都是尽量满足设计，如果不能满足的话就尽量贴近，不得已（性能之类的问题）才会砍掉某个浏览器版本上的需求。

#### 8、有哪些的隐藏内容的方法（如果同时还要保证屏幕阅读器可用呢？）

常用的隐藏方法有两种：

1. 对于 `display: none`，即便是读屏设备也会忽略掉这些内容（其实浏览器对于设置为 `display: none` 的元素不会进行渲染）。
2. 而设置为 `visibility: hidden` 的元素，他仍然存在于文档中，占据本来的位置。

对于屏幕阅读器的优化，可以用媒体查询来完成，@`media speech` 用于语音输出的读屏设备。

```css
@media speech {
    /* media-specify rules */
}
```

#### 9、你用过栅格系统吗？如果使用过，你最喜欢哪种？

用过。栅格系统应该依据具体的情形而使用，能与当前项目深度结合最好，不要为使用栅格系统而使用栅格系统。掌握栅格系统的解决问题的思维方式很重要。

参考：http://yianbin.gitgub.io/bitty-grid-system

#### 10、你用过媒体查询，或针对移动端的布局 CSS 吗？

使用媒体查询实现响应话网页设计（RWD），同时是移动端优先：

```css
@media all and (min-width: 800px) {
    .container {
        width: 740px;
    }
}
@media all and (min-width: 1000px) {
    .container {
        width: 880px;
    }
}
@media all and (min-width: 1280px) {
    .container {
        width: 1200px;
    }
}
```

#### 11、你熟悉 SVG 样式的书写吗？

参考：https://developer.mozilla.org/zh-CN/docs/Web/SVG/Tutorial

#### 12、如何优化网页的打印样式？

使用媒体查询 `@media print`，针对打印设置单独的样式。

#### 13、在书写高效 CSS 时会有哪些问题需要考虑？

1. 避免嵌套层级太深；
2. 尽量使用 `.class` 给页面元素添加样式，`#id` 的权重太大了；
3. 优化选择器

#### 14、使用 CSS 预处理器（SASS，Compass，Stylus，LESS）的优缺点有哪些？描述下你曾经使用过的 CSS 预处理的优缺点。

优点：1、解决传统 CSS 无法使用变量、算术计算、条件判断等缺陷；2、Mixin 混入技术；3、提高代码开发效率。

缺点：需要额外学习成本。

#### 15、如果设计中使用了非标准的字体，你该如何去实现？

Webfonts（字体服务例如：Google Fonts，Typekit 等等），或者通过 `@font-face` 设置。

#### 16、解释下浏览器是如何判断元素是否匹配某个 CSS 选择器？

#### 17、解释一下你对盒模型的理解，以及如何在 CSS 中告诉浏览器使用不同的盒模型来渲染你的布局。

文档中的每个元素被描绘为矩形盒子。确定其大小，属性——比如颜色、背景、边框，及其位置是渲染引擎的目标。CSS 下这些矩形盒子由标准盒模型描述。这个模型描述元素内容占用空间。盒子有四个边界：外边距边界 margin edge，边框边界 border edge，内边距边界 padding edge 与内容边界 content edge。

![标准盒模型](http://yianbin.qiniudn.com/fe-box-modal.jpg)

在 CSS 中可以使用 `box-sizing` 来改变盒模型：

1. `border-box`：默认值，标准盒模型。 `width` 与 `height` 是内容区的宽与高， 不包括边框，内边距，外边距。
2. `padding-box`：`width` 与 `height` 包括内边距，不包括边框与外边距。
3. `border-box`： `width` 与 `height` 包括内边距与边框，不包括外边距。这是 IE 怪异模式（Quirks mode）使用的盒模型 。

#### 18、请解释一下 `* { box-sizing: border-box }` 的作用, 并且说明使用它有什么好处？

设置为 `box-sizing: border-box` 的元素在计算宽度和高度时，会包括内边距与边框。

#### 19、请罗列出你所知道的 `display` 属性的全部值

`display` 是 CSS 中最重要的用于控制布局的属性。每个元素都有一个默认的 `display` 值，这与元素的类型有关。对于大多数元素它们的默认值通常是 `block` 或 `inline`。一个 `block` 元素通常被叫做块级元素。一个 `inline` 元素通常被叫做行内元素。

1. `block`：一个块级元素会新开始一行并且尽可能撑满容器。`div` 是一个标准的块级元素。其他常用的块级元素包括 `p`、`form` 和 HTML5 中的新元素：`header`、`footer`、`section` 等等。
2. `inline`：一个行内元素可以在段落中 `<span>像这样</span>` 包裹一些文字而不会打乱段落的布局。`a` 元素是最常用的行内元素，它可以被用作链接。
3. `inline-block`：`inline-block` 的元素在元素外表现的像行内元素，其盒模型的宽度为元素的实际宽度，而在元素内部表现为一个块级元素，可以设置宽高。
4. `table` 类：与表格 `table` 相关的。
5. `flexbox`：弹性布局，参考：http://www.html5rocks.com/zh/tutorials/flexbox/quick/
6. `none`：通常被 JavaScript 用来在不删除元素的情况下隐藏或显示元素。它和 `visibility` 属性不一样。把 `display` 设置成 `none` 不会保留元素本该显示的空间，但是 `visibility: hidden` 还会保留。

#### 20、请解释一下 `inline` 和 `inline-block` 的区别？

#### 21、请解释一下 `relative`、`fixed`、`absolute` 和 `static` 元素的区别

`static` 是 `position` 属性的默认值，任何 `position` 为 `static` 的元素不会被特殊的定位。相对定位 `relative` 表现的和 `static` 一样，除非你添加了一些额外的属性（`top` 、`right`、`bottom` 和 `left`）。一个固定定位（`position` 属性的值为 `fixed`）元素会相对于视窗来定位，这意味着即便页面滚动，它还是会停留在相同的位置。和 `relative` 一样，`top` 、`right`、`bottom` 和 `left` 属性都可用。一个固定定位元素不会保留它原本在页面应有的空隙。`absolute` 是最棘手的 `position` 值。`absolute` 与 `fixed` 的表现类似，除了它不是相对于视窗而是相对于最近的被定位的（`position` 值不是 `static`）祖先元素。

#### 22、你目前在使用哪一套CSS框架，或者在产品线上使用过哪一套？（Bootstrap, PureCSS, Foundation 等等）。如果有，请问是哪一套？如果可以，你如何改善 CSS 框架？

使用过 Bootstrap、Flat UI 等。

#### 24、请问你有使用过 CSS Flexbox 或者 Grid specs 吗？如果有，请问在性能和效率的方面你是怎么看的？

不会