# CSS 规范

# 参考
+ BEM: https://juejin.im/post/5b925e616fb9a05cdd2ce70d
+ SMACSS: https://juejin.im/post/5ba234c85188255c38535a47
+ NEC: http://nec.netease.com/standard/css-sort.html
+ weui: https://weui.io/#/

参考流行的CSS规范，结合实际情况，拟写了一套简约的规范，以供使用。

# 类别规范
CSS类别规则
+ 1 页面 （Page）：页面
+ 2 布局 （Grid）：布局，通常有头部、主体、主栏、侧栏、尾部
+ 3 组件 (Unit) | 模块 (Modules)：可以重复使用的独立的模块，比如按钮、loading、toast、弹窗
+ 4 拓展状态 (Extend State)：颜色、形状、边框、阴影
+ 5 功能 (Function)：功能类，例如清除浮动，文本溢出显示省略号
+ 6 钩子 (JavaScript)：作为js的钩子，纯属给元素绑定事件，不给改类名添加任何样式

# 命名规范

## 1 页面 （Page）
> 通常以'page-'为类前缀，每个页面只有一个'.page-'的命名，作为命名空间

结构如下：

```html
<!-- 假设页面为首页 -->
<div class="page-index">
  <!-- 内容 -->
</div>
```
## 2 布局 （Grid）
> 通常以'g-'为类前缀

结构如下：
```html
<!-- 头部 -->
<div class="g-header">
</div>
<!-- 边栏 -->
<div class="g-sidebar">
</div>
<!-- 主体内容 -->
<div class="g-content">
</div>
<!-- 底部 -->
<div class="g-footer">
</div>
```

## 3 组件 (Unit) | 模块 (Modules)
> 通常以'u-'为类前缀，作为组件或者模块

结构如下：
```html
<!-- 按钮 -->
<a href="javascript:;" class="u-btn">按钮<a>
<!-- 输入框 -->
<input class="u-input" placeholder="输入框"/>

<!-- 卡片模块 -->
<section class="u-card tools-box">
  <h4 class="card-title-box">
    <p class="card-title">我的家庭</p>
  </h4>
</section>
<!-- 卡片模块 -->
<section class="u-card news-box">
</section>
```
样式如下：
```css
/* button */
.u-btn {
  display: inline-block;
  vertical-align: middle;
  line-height: 80px;
  font-size:32px;
  text-align: center;
  font-weight:400;
  color:rgba(255,255,255,1);
  background:linear-gradient(to right, #fd8261, #ffac74);
  box-shadow:0px 0px 10px 0px rgba(89,149,239,0.1);
  border-radius:8px;
}
/* 输入框 */
.u-input {
  padding-left: 30px;
  font-size:32px;
  font-weight:400;
  color:#383838;
  line-height:50px;
}
/* 卡片模块 */
.u-card {
  position: relative;
  margin: 30px 20px 0;
  background: rgba(255, 255, 255, 1);
  box-shadow: 0px 0px 20px 0px rgba(0, 0, 0, 0.2);
  border-radius: 10px;
  transition: all 0.5s linear;
  /* 卡片标题 */
  .card-title-box {
    position: absolute;
    top: 0;
    left: 0;
    font-size: 0;
    display: flex;
    align-items: center;

    .card-title {
      padding: 0 26px;
      font-size: 30px;
      font-weight: 500;
      color: rgba(255, 255, 255, 1);
      line-height: 60px;
      background: #fe5129;
      box-shadow: 0px 0px 20px 0px rgba(255, 255, 255, 0.4);
      border-radius: 10px 0 34px 0;
    }
  }
}
```
## 4 拓展状态 (Extend State)
> 通常以'e-'为类前缀
例如有个按钮组件(.u-btn)，按钮有几种状态，分别是宽度撑满父级，带边框，不可点击

结构如下：
```html
<!-- 宽度撑满父级的按钮 -->
<div class="u-btn e-full">
  按钮
</div>
<!-- 带边框的按钮 -->
<div class="u-btn e-border">
  按钮
</div>
<!-- 宽度撑满父级、不可点击的按钮 -->
<div class="u-btn e-full e-disable">
  按钮
</div>
```

样式如下：
```scss
/* button */
.u-btn {
  display: inline-block;
  vertical-align: middle;
  line-height: 80px;
  font-size:32px;
  text-align: center;
  font-weight:400;
  color:rgba(255,255,255,1);
  background:linear-gradient(to right, #fd8261, #ffac74);
  box-shadow:0px 0px 10px 0px rgba(89,149,239,0.1);
  border-radius:8px;
  /* 宽度撑满父级 */
  &.e-full {
    width: 100%;
  }
  /* 带边框 */
  &.e-border {
    color:FF4041;
    background:rgba(255,255,255,1);
    border: 2px solid FF4041;
    border-radius: 8px;
  }
  /* 不可点击 */
  &.e-disable {
    background: #ccc;
    border: none;
    pointer-events: none;
  }
}
```
## 5 功能 (Function)
> 通常以'f-'为类前缀
通常用以处理功能性的样式，例如清除浮动，显示，隐藏

样式如下：
```css
/* 左浮动 */
.f-left{float:left}
/* 右浮动 */
.f-right{float:right}
/* 清除浮动 */
.f-clearfix{zoom:1;clear:both}
.f-clearfix:after{visibility:hidden;display:block;font-size:0;content:" ";clear:both;height:0}
/* 显示，隐藏 */
.f-hide{display:none}
.f-show{display:block}
/* 溢出文本自动省略号*/
.f-ellipsis {
  overflow: hidden;
  white-space: nowrap;
  text-overflow: ellipsis;
  word-break: keep-all;
}
```
## 6 钩子 (JavaScript)
> 通常以'j-'为类前缀
纯属给元素绑定事件，不带任何css样式

结构如下：

```html
<div class="j-get-coupon"></div>
```

js如下：
```javascript
// 绑定事件
document.querySelector('.j-get-coupon').addEventListener('click', function() {}, false)
```

# 原则
+ css选择器中避免使用标签名，样式与标签结构无关，导航应该类似于 .site-nav 而不是 #header ul
+ 不使用 ID
+ 避免使用 !important，除去某些极特殊的情况，尽量不要不要使用 !important


# 代码风格
## 1 缩进
使用 2 个空格做为一个缩进层级
## 2 空格
选择器 与 { 之间必须包含空格
```css
.selector { /* good */
}
.selector{ /* bad */
}
```
属性名 与之后的 : 之间不允许包含空格， : 与 属性值 之间必须包含空格
```css
margin: 0; /* good */
margin:0; /* bad */

```
## 3 属性缩写
在可以使用缩写的情况下，尽量使用属性缩写，除了需要用javascript动态控制样式，例如vue的动态控制style
```css
/* 文字 */
.selector {
  /* good */
  font: normal small-caps bold 14px/1.5em -apple-system-font, "Helvetica Neue", sans-serif;

  /* bad */
  font-style: normal;
  font-variant: small-caps;
  font-weight: bold;
  font-size: 14px;
  line-height: 1.5em;
  font-family: -apple-system-font, "Helvetica Neue", sans-serif;
}


/* 背景
background简写的顺序如下:
bg-color || bg-image || bg-position [ / bg-size]? || bg-repeat || bg-attachment || bg-origin || bg-clip
*/
.selector {
  /* good */
  background: #fff url(header_bg.jpg) no-repeat fixed left top;

  /* bad */
  background-color: #fff;
  background-image:  url(header_bg.jpg);
  background-repeat: no-repeat;
  background-attachment: fixed;
  background-position: left top;
}

.selector {
  /* good */
  background: url(image.png) 40px 10px/110px 110px no-repeat content-box;

  /* bad */
  background-image: url(image.png);
  background-position-x: 40px;
  background-position-y: 10px;
  background-size: 110px 110px;
  background-repeat-x: no-repeat;
  background-repeat-y: no-repeat;
  background-attachment: initial;
  background-origin: content-box;
  background-clip: content-box;
  background-color: initial;
}

```
## 4 属性书写顺序
建议按照以下顺序书写css属性，一定程度上能优化性能
+ （1）formatting model【布局方式、位置】(position / top / right / bottom / left / float / display / overflow等)
+ （2）box model【盒子模型】（margin / padding / width / height / border等）
+ （3）typographic【文字系列】（font / line-height / letter-spacing / text-align等）
+ （4）visual【形态】（background / color / transition / list-style等）
代码示例
```css
.selector {
   /* formatting model: positioning schemes / offsets / z-indexes / display / ...  */
    position: absolute;
    top: 50px;
    left: 0;
    overflow-x: hidden;

    /* box model: sizes / margins / paddings / borders / ...  */
    width: 200px;
    padding: 5px;
    border: 1px solid #ddd;

    /* typographic: font / aligns / text styles / ... */
    font-size: 14px;
    line-height: 20px;

    /* visual: colors / shadows / gradients / ... */
    background: #f5f5f5;
    color: #333;
    transition: color 1s;
}
```
## 5 z-index
层级规范：
+ dialog 30
+ loading 40
+ toast 50

额外，在可控环境下，期望显示在最上层的元素，z-index 指定为 999999
