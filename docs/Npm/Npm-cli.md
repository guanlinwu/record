# Npm 开发自己的cli命令

## 常用组件
+ fs-extra fs升级版
+ chalk 终端文字加颜色js组件
+ boxen Create boxes in the terminal
+ clui spinners、sparklines、progress bars图样显示组件
+ shelljs node.js运行shell命令组件
+ blessed-contrib 命令行可视化组件
+ lnquirer 命令行交互信息收集组件
+ prompts 命令行交互信息收集组件
+ figlet FIGlet is a program that creates large characters out of ordinary screen characters
+ commander CLI常用开发框架
+ yargs
+ minimist 处理参数的小工具
+ semver 通常用来比较node版本，然后对node进行升级
+ semver-diff Get the diff type of two semver versions: 0.0.1 0.0.2 → patch
+ progress 进度条
```javascript
// 来自vue-cli3
const requiredVersion = require('../package.json').engines.node

function checkNodeVersion (wanted, id) {
  if (!semver.satisfies(process.version, wanted)) {
    console.log(chalk.red(
      'You are using Node ' + process.version + ', but this version of ' + id +
      ' requires Node ' + wanted + '.\nPlease upgrade your Node version.'
    ))
    process.exit(1)
  }
}

checkNodeVersion(requiredVersion, 'vue-cli')
```
+ clui to add some additional visual components
+ figlet 用_｜/\输出英文
+ clear 清除控制台
+ configstore  easily loads and saves config without you having to think about where and how.本地缓存
+ @octokit/rest — a GitHub REST API client for Node.js
+ simple-git — a tool for running Git commands in a Node.js application
+ touch — a tool for implementating the Unix touch command.
+ listr Terminal task list
+ execa Process execution for humans
+ update-check 检查是否需要更新版本
```javascript
const pkg = require('../package.json')
const chalk = require('chalk')
const boxen = require('boxen')
const checkForUpdate = require('update-check')

const updateCheck = async () => {
	let update = null

  try {
    update = await checkForUpdate(pkg)
  } catch (err) {
    console.error(`Failed to check for updates: ${err}`)
  }

  if (update) {
    let installCommand = `npm i -g @linahome/cli`
    let message = 'Update available ' + chalk.dim(pkg.version) + chalk.reset(' → ') + chalk.green(update.latest) + ' \nRun ' + chalk.cyan(installCommand) + ' to update'
    let boxenOpts = {
			padding: 1,
			margin: 1,
			align: 'center',
			borderColor: 'yellow',
			borderStyle: 'double'
    }
    const result = boxen(message, boxenOpts)

    console.log(result)
  }
}
```
+ update-notifier 检查是否需要更新版本
+ latest-version Get the latest version of an npm package
+ package-json Get metadata of a package from the npm registry
+ ora loading

+ git克隆 用 --depth=1， depth用于指定克隆深度，为1即表示只克隆最近一次commit，体积很小
+ mem-fs-editor  mem-fs  File edition helpers working on top of mem-fs
 mem-fs  对文件进行读取，存入内存中
 mem-fs-editor 是对内存中的文件信息，使用ejs语法进行编译。最后调用commit方法输出最终文件
+ edit-json-file 编辑json
+ load-json-file 远程获取json文件
+ node-fetch 请求
+ flyio 请求


## 可能可以留意的值
process.execPat
process.env

## package.json
```json
{
    // 模块系统的名字，如require('npmhelloworld')
    "name": "npmhelloworld",
    "bin": {
      "nhw": "index.js" // nhw就是命令名 ，index.js就是入口
    },
    // 加入 安装的时候, 就会有-g的提示了
    "preferGlobal": true,
    "license": "ISC"
}
```