# CSS 常用集合片段收集

## 文本溢出显示省略号

### 文本溢出显示省略号
```css
/*文本溢出显示省略号*/
.ellipsis {
  overflow: hidden;
  white-space: nowrap;
  word-break: keep-all;
  text-overflow: ellipsis;
}
```
### 超过N行后就显示省略号
```css
/*超过N行后就显示省略号，这里n=2 不要定死高度*/
.showNRow {
  overflow: hidden;
  text-overflow: ellipsis;
  display: -webkit-box;
  -webkit-line-clamp: 2;
  -webkit-box-orient: vertical;
  white-space: normal;
  word-break: break-all;
}

```

## 重置外形

### 去除select外形
```css
/*去除select外形*/
{
  -webkit-appearance: none; /*去除 select 表单右侧箭头*/
  border: none;
  outline: none;
}
```

### 去除input[type="number"]的箭头
```css
/*去除input[type="number"]的箭头*/
input::-webkit-outer-spin-button,
input::-webkit-inner-spin-button {
  -webkit-appearance: none;
}

input[type="number"] {
  -moz-appearance: textfield;
}
```

### 去除移动端touch事件阴影
```css
/*去除移动端touch事件阴影*/
* {
  -webkit-tap-highlight-color: rgba(0, 0, 0, 0);
  -webkit-tap-highlight-color: transparent;
}
```

### 设置input placeholder的颜色
```css
/*设置input placeholder的颜色*/
::-webkit-input-placeholder {}
::-moz-input-placeholder {}
::-ms-input-placeholder {}
::input-placeholder {}
```

### 改变input 光标颜色
```css
input {
  /*改变input 光标颜色*/
  caret-color: red;
}
```

## 1px细线
1px细线的方法很多，暂时记录常用的
```css
/*1px 细线 */
.line {
  content: "";
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  border-top: 1px solid #c8c7cc;
  -webkit-transform: scaleY(.5);
  -webkit-transform-origin: 0 0;
  pointer-events: none;
}

```

```css

/*1px 边框 可以支持到圆角*/
.line {
  position: relative;
}
.line::before {
  content: "";
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  border-color: #000;
  border-width: 1px;
  border-style: solid;
  width: 200%;
  height: 200%;
  border-radius: 20px;
  -webkit-transform: scale(.5);
  -webkit-transform-origin: 0 0;
  pointer-events: none;
}
```

```scss
/**
* 1px细线
* border-width-1px(top,right,bottom,left, border-color, border-radius);
* top,right,bottom,left 值为 1 或者 0;
* @include border-width-1px(0, 0, 2, 0, #f57c38);
*/
@mixin border-width-1px($border-width-top: 0, $border-width-right: 0, $border-width-bottom: 0, $border-width-left: 0, $border-color: $g-bordercolor, $border-radius: 0){
  position: relative;
  border-color: $border-color;
  border-width: #{$border-width-top}Px #{$border-width-right}Px #{$border-width-bottom}Px #{$border-width-left}Px; // ignored  postcss-pxtorem
  border-style: solid;
  @if $border-radius != 0{
    border-radius: $border-radius/2/40px * 1rem;
  }

  @media
  only screen and (-webkit-min-device-pixel-ratio: 2),
  only screen and (   min--moz-device-pixel-ratio: 2),
  only screen and (     -o-min-device-pixel-ratio: 2/1),
  only screen and (        min-device-pixel-ratio: 2),
  only screen and (                min-resolution: 192dpi),
  only screen and (                min-resolution: 2dppx) {
    border: none;
    &::before{
      content: "";
      position: absolute;
      top: 0;
      left: 0;
      right: 0;
      bottom: 0;
      border-color: $border-color;
      border-width: #{$border-width-top}Px #{$border-width-right}Px #{$border-width-bottom}Px #{$border-width-left}Px; // ignored  postcss-pxtorem
      border-style: solid;
      width: 200%;
      height: 200%;
      transform: scale(.5);
      transform-origin: 0 0;
      pointer-events: none;
      @if $border-radius != 0{
        border-radius: $border-radius;
      }
    }
  }
}
```

## 背景斜线
```css
/*背景斜线*/
.bgline45double {
  -webkit-gradient(linear, 100% 0, 0 100%, color-stop(.25, rgba(240, 240, 240, .2)), color-stop(.25, transparent), color-stop(.5, transparent), color-stop(.5, rgba(240, 240, 240, .2)), color-stop(.75, rgba(240, 240, 240, .2)), color-stop(.75, transparent), to(transparent)),
  -webkit-gradient(linear, 0 100%, 100% 0, color-stop(.25, rgba(240, 240, 240, .2)), color-stop(.25, transparent), color-stop(.5, transparent), color-stop(.5, rgba(240, 240, 240, .2)), color-stop(.75, rgba(240, 240, 240, .2)), color-stop(.75, transparent), to(transparent));
  background-size: 14px 14px;
}

.bgline45 {
  background-image: -webkit-gradient(linear, 0 100%, 100% 0, color-stop(.25, rgba(240, 240, 240, .2)), color-stop(.25, transparent), color-stop(.5, transparent), color-stop(.5, rgba(240, 240, 240, .2)), color-stop(.75, rgba(240, 240, 240, .2)), color-stop(.75, transparent), to(transparent));
  background-size: 14px 14px;
}

```


```css
/*bug
1. line-height，要块级才可以定义
2. 解决内层margin 不撑开外层， 外层加overflow:hidden; 或者外层padding: 1;
*/
```

## 悬浮背景，支持IOS
```css
/*background-attachment:fixed ios 无效 解决方法*/
.u-fix-img {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  margin: 0 auto;
  z-index: -1;
  background-color: transparent;
  background-repeat: repeat;
  height: 100%;
  width: 100%;
}
```

## 移动设备上是否使用滚动回弹效果
```css
/*控制元素在移动设备上是否使用滚动回弹效果*/
.elemet {
  white-space: nowrap;
  -webkit-overflow-scrolling: touch; // 控制元素在移动设备上是否使用滚动回弹效果
  overflow-x: scroll;
  overflow-y: hidden;
}

```