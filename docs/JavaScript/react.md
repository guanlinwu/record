# React

## 渲染的时候都会触发待点击事件
很多人经常忘记编写 () =>，而写成了 onClick={alert('click')}，这种常见的错误会导致每次这个组件渲染的时候都会触发弹出框。

```javascript
class Square extends React.Component {
 render() {
   return (
     <button className="square" onClick={() => alert('click')}>
       {this.props.value}
     </button>
   );
 }
}
```

## webpack
### Unexpected token import
如果用了按需加载 @loadable/component 组件，则要安装 @babel/plugin-syntax-dynamic-import，构建支持动态import，不然会提示‘Unexpected token import’