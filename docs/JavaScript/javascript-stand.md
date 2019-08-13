# JavaScript 代码规范

## 一 基本书写

> 使用两个空格进行缩进，不要混合使用空格与制表符作为缩进

```javascript
function func (param) {
  console.log('func', param) // ✓ 正确
  console.log('func', param) // ✗ 错误
}
```

> 不要使用多余空格

```javascript
let number =    1234 // ✗ 错误
let number =    1234    // ✗ 错误
let number =    1234 //     ✗ 错误
let number = 1234 // ✓ 正确
```

> 不要在句末使用分号

```javascript
let string = 'a' // ✓ 正确
let string = 'a'; // ✗ 错误
```

> 字符串统一使用单引号

```javascript
console.log('this is a string')
/*
 * 如果遇到需要转义的情况，请按如下三种写法书写
 */
const str1 = 'this is a "string"'
const str2 = 'this is a \'string\''
const str3 = `this is a 'string'`
```

> 代码块中避免多余留白

```javascript
if (login) { // ✗ 错误

  const userInfo = getInfo()

}

if (login) { // ✓ 正确
  const userInfo = getInfo()
}
```

> 关键字后面加空格

```javascript
if (condition) { // ✓ 正确
  ...
}
if(condition) { // ✗ 错误
  ...
}
```

> 函数声明时括号与函数名间加空格

```javascript
function func (arg) {
  ...
} // ✓ 正确
function func(arg) {
  ...
} // ✗ 错误

execute(function () {
  ...
}) // ✓ 正确
execute(function() {
  ...
}) // ✗ 错误

```

> 展开运算符与它的表达式间不要留空白

```javascript
func(... args) // ✗ 错误
func(...args) // ✓ 正确
```

> 遇到分号时，分号后留空格，分号前不留空格

```javascript
for (let i = 0 ;i < items.length ;i++) {
  ...
} // ✗ 错误
for (let i = 0; i < items.length; i++) {
  ...
} // ✓ 正确
```

> 代码块首尾留空格

```javascript
if (login){ // ✗ 错误
  const userInfo = getInfo()
}
if (login) { // ✓ 正确
  const userInfo = getInfo()
}
```

> 圆括号间不留空格

```javascript
func( params ) // ✗ 错误
func(params) // ✓ 正确

```

> 一元运算符前面跟一个空格

```javascript
typeof!value // ✗ 错误
typeof !value // ✓ 正确

```

> 注释首尾留空格

```javascript
//comment // ✗ 错误
// comment // ✓ 正确

/*comment*/ // ✗ 错误
/* comment */ // ✓ 正确
```

> 模板字符串中变量前后不加空格

```javascript
const message = `Hello, ${ name }` // ✗ 错误
const message = `Hello, ${name}` // ✓ 正确
```

> 逗号后面加空格

```javascript
// ✓ 正确
const list = [1, 2, 3, 4]
function func (param1, param2) { ... }
```

```javascript
// ✗ 错误
const list = [1,2,3,4]
function func (param1,param2) { ... }
```

> 不允许有连续多行空行

```javascript
// ✓ 正确
const value = 'hello world'
console.log(value)
```

```javascript
// ✗ 错误
const value = 'hello world'



console.log(value)
```

> 单行代码块两边加空格

```javascript
function func () {return true}    // ✗ 错误
function func () { return true }  // ✓ 正确
if (condition) { return true }  // ✓ 正确
```

> 点号操作符须与属性需在同一行

```javascript
console.log('hello') // ✓ 正确

console.
  log('hello') // ✗ 错误

console
  .log('hello') // ✓ 正确
```

> 函数调用时标识符与括号间不留间隔

```javascript
console.log ('hello') // ✗ 错误
console.log('hello') // ✓ 正确
```

> 键值对当中冒号与值之间要留空白

```javascript
const obj = { 'key' : 'value' } // ✗ 错误
const obj = { 'key' :'value' } // ✗ 错误
const obj = { 'key':'value' } // ✗ 错误
const obj = { 'key': 'value' } // ✓ 正确
```

> 字符串拼接操作符 (Infix operators) 之间要留空格

```javascript
// ✓ 正确
const x = 2
const message = 'hello, ' + name + '!'
```

```javascript
// ✗ 错误
const x=2
const message = 'hello, '+name+'!'
```

> 不要使用多行字符串

```javascript
const message = 'Hello \
                 world' // ✗ 错误
```

## 二 变量定义

> 使用 const/let 定义变量
当前作用域不需要改变的变量使用 const，反之则使用 let

> 每个 const/let 关键字单独声明一个变量

> 不要重复声明变量

> 不要使用 undefined 来初始化变量

> 对于变量和函数名统一使用驼峰命名法

```javascript
function my_function () { } // ✗ 错误
function myFunction () { } // ✓ 正确

const my_var = 'hello' // ✗ 错误
const myVar = 'hello' // ✓ 正确
```

> 不要定义未使用的变量

```javascript
function myFunction () {
  const result = something() // ✗ 错误
}
```

## 三 基本类型

> 使用 isNaN() 检查 NaN

```javascript
if (price === NaN) { }      // ✗ 错误
if (isNaN(price)) { }       // ✓ 正确
```

## 四 对象与数组

> 对象中定义了存值器，一定要对应的定义取值器

```javascript
const person = {
  set name (value) { // ✗ 错误
    this._name = value
  }
}

const person = {
  set name (value) {
    this._name = value
  },
  get name () { // ✓ 正确
    return this._name
  }
}
```

> 使用数组字面量而不是构造器

```javascript
const numArray = new Array(1, 2, 3)   // ✗ 错误
const numArray = [1, 2, 3]            // ✓ 正确
```

> 不要扩展原生对象

```javascript
Object.prototype.name = 'name' // ✗ 错误
```

> 对象属性换行时注意统一代码风格

```javascript
const user = {
  name: 'Jane Doe', age: 30,
  username: 'jdoe86' // ✗ 错误
}

const user = { name: 'Jane Doe', age: 30, username: 'jdoe86' } // ✓ 正确

const user = {
  name: 'Jane Doe',
  age: 30,
  username: 'jdoe86'
}
```

> 避免使用不必要的计算值作对象属性

```javascript
const user = { ['name']: 'John Doe' } // ✗ 错误
const user = { name: 'John Doe' } // ✓ 正确
```

## 五 函数

> 避免使用 arguments.callee 和 arguments.caller

```javascript
function foo (n) {
  if (n <= 0) return
  arguments.callee(n - 1) // ✗ 错误
}

function foo (n) {
  if (n <= 0) return
  foo(n - 1)
}
```

> 避免多余的函数上下文绑定

```javascript
const name = function () {
  getName()
}.bind(user) // ✗ 错误

const name = function () {
  this.getName()
}.bind(user) // ✓ 正确
```

> 不要使用 eval()

```javascript
eval( "var result = user." + propName ) // ✗ 错误
```

> 不要使用多余的括号包裹函数

```javascript
const func = (function () { })   // ✗ 错误
const func = function () { }     // ✓ 正确
```

> 避免对声明过的函数重新赋值

```javascript
function func () { }
func = otherFunc // ✗ 错误
```

> 注意隐式的 eval()

```javascript
setTimeout("alert('Hello world')") // ✗ 错误
setTimeout(function () { alert('Hello world') }) // ✓ 正确
```

> 嵌套的代码块中禁止再定义函数

```javascript
if (condition) {
  function func () {} // ✗ 错误
}
```

> 自调用匿名函数 (IIFEs) 使用括号包裹

```javascript
const getName = function () { }() // ✗ 错误

const getName = (function () { }()) // ✓ 正确
const getName = (function () { })() // ✓ 正确

```

> 使用 Promise 或者 async functions 来实现异步编程, 不使用 Generator 函数语法

```javascript
function* helloWorldGenerator() { // ✗ 错误
  yield 'hello';
  yield 'world';
  return 'ending';
}
```
## 六 类定义

> 类名要以大写字母开头

```javascript
class animal {}
const dog = new animal() // ✗ 错误

class Animal {}
const dog = new Animal() // ✓ 正确
```

> 子类的构造器中一定要调用 super

```javascript
class Dog {
  constructor () {
    super() // ✗ 错误
  }
}

class Dog extends Mammal {
  constructor () {
    super() // ✓ 正确
  }
}
```

> 使用 this 前请确保 super() 已调用

```javascript
class Dog extends Animal {
  constructor () {
    this.legs = 4 // ✗ 错误
    super()
  }
}
```

> 无参的构造函数调用时要带上括号

```javascript
function Animal () {}
const dog = new Animal // ✗ 错误
const dog = new Animal() // ✓ 正确
```

> new 创建对象实例后需要赋值给变量

```javascript
new Character() // ✗ 错误
const character = new Character() // ✓ 正确
```

## 七 模块

> 同一模块有多个导入时一次性写完

```javascript
import { module1 } from 'module'
import { module2 } from 'module' // ✗ 错误

import { module1, module2 } from 'module' // ✓ 正确
```

> import, export 和解构操作中，禁止赋值到同名变量

```javascript
import { config as config } from './config' // ✗ 错误
import { default as appConfig } from './config' // ✗ 正确
import { config } from './config' // ✓ 正确
```

## 八 语句

> 避免在 return 语句中出现赋值语句

```javascript
function sum (a, b) {
  return result = a + b // ✗ 错误
}
```

> 禁止使用 with

> 禁止使用 标签语句

```javascript
label:
  while (true) {
    break label // ✗ 错误
  }
```

> return，throw，continue 和 break 后不要再跟代码

```javascript
function doSomething () {
  return true
  console.log('never called') // ✗ 错误
}
```

## 九 逻辑与循环

> 始终使用 === 替代 ==
例外： obj == null 可以用来检查 null || undefined


```javascript
if (name === 'John') // ✓ 正确
if (name == 'John') // ✗ 错误

if (name !== 'John') // ✓ 正确
if (name != 'John') // ✗ 错误
```

> if/else 关键字要与花括号保持在同一行

```javascript
// ✓ 正确
if (condition) {
  // ...
} else {
  // ...
}
```

```javascript
// ✗ 错误
if (condition)
{
  // ...
}
else
{
  // ...
}
```

> 多行 if 语句的的括号不能省略

```javascript
// ✓ 正确
if (condition) console.log('done')
// ✓ 正确
if (condition) {
  console.log('done')
}
// ✗ 错误
if (condition)
  console.log('done')
```

> 对于三元运算符 ? 和 : 与他们所负责的代码处于同一行

```javascript
// ✓ 正确
const location = env.development ? 'localhost' : 'www.prop.com'

// ✓ 正确
const location = env.development
  ? 'localhost'
  : 'www.prop.com'

// ✗ 错误
const location = env.development ?
  'localhost' :
  'www.prop.com'
```

> 如果有更好的实现，尽量不要使用三元表达式

```javascript
let score = val ? val : 0 // ✗ 错误
let score = val || 0 // ✓ 正确
```

> switch 一定要使用 break 来将条件分支正常中断

```javascript
switch (filter) {
  case 1:
    doSomething() // ✗ 错误
  case 2:
    doSomethingElse()
}

switch (filter) {
  case 1:
    doSomething()
    break // ✓ 正确
  case 2:
    doSomethingElse()
}

switch (filter) {
  case 1:
    doSomething()
    // fallthrough // ✓ 正确
  case 2:
    doSomethingElse()
    break // ✓ 正确
}
```

## 十 错误处理

> 不要丢掉异常处理中 err 参数

```javascript
// ✓ 正确
execute(function (err) {
  if (err) throw err
  window.alert('done')
})
```

```javascript
// ✗ 错误
execute(function (err) {
  window.alert('done')
})
```

> 用 throw 抛错时，抛出 Error 对象而不是字符串

```javascript
throw 'error' // ✗ 错误
throw new Error('error') // ✓ 正确
```

> 使用 Promise 一定要捕捉错误

```javascript
asyncTask('google.com')
.catch(err => console.log(err)) // ✓ 正确
```