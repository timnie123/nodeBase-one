## Node基础第一讲

![1598881412148](./1598881412148.png)

### 简介

Node.js 是一个开源与跨平台的 JavaScript 运行时环境。 它是一个可用于几乎任何项目的流行工具！

Node.js 在浏览器外运行 V8 JavaScript 引擎（Google Chrome 的内核）。 这使 Node.js 表现得非常出色。

Node.js 应用程序运行于单个进程中，无需为每个请求创建新的线程。 Node.js 在其标准库中提供了一组异步的 I/O 原生功能（用以防止 JavaScript 代码被阻塞），并且 Node.js 中的库通常是使用非阻塞的范式编写的（从而使阻塞行为成为例外而不是规范）。

当 Node.js 执行 I/O 操作时（例如从网络读取、访问数据库或文件系统），Node.js 会在响应返回时恢复操作，而不是阻塞线程并浪费 CPU 循环等待。

这使 Node.js 可以在一台服务器上处理数千个并发连接，而无需引入管理线程并发的负担（这可能是重大 bug 的来源）。

Node.js 具有独特的优势，因为为浏览器编写 JavaScript 的数百万前端开发者现在除了客户端代码之外还可以编写服务器端代码，而无需学习完全不同的语言。

在 Node.js 中，可以毫无问题地使用新的 ECMAScript 标准，因为不必等待所有用户更新其浏览器，你可以通过更改 Node.js 版本来决定要使用的 ECMAScript 版本，并且还可以通过运行带有标志的 Node.js 来启用特定的实验中的特性。

总之Node.js 是一个基于 Chrome V8 引擎的 [JavaScript](https://baike.baidu.com/item/JavaScript/321142) 运行环境。 Node.js 使用了一个事件驱动、非阻塞式 I/O 的模型。



### 与浏览器的区别

浏览器和 Node.js 均使用 JavaScript 作为其编程语言。

构建运行于浏览器中的应用程序与构建 Node.js 应用程序完全不同。

尽管都是 JavaScript，但一些关键的差异使体验相当不同。

从广泛使用 JavaScript 的前端开发者的角度来看，Node.js 应用程序具有巨大的优势：使用单一语言轻松编程所有一切（前端和后端）。

你会拥有巨大的机会，因为全面、深入地学习一门编程语言并通过使用同一语言完成 web（无论是在客户端还是在服务器）上的所有工作是非常困难的，你会处于独特的优势地位。

不同的还有生态系统。

在浏览器中，大多数时候做的是与 DOM 或其他 Web 平台 API（例如 Cookies）进行交互。 当然，那些在 Node.js 中是不存在的。 没有浏览器提供的 `document`、`window`、以及所有其他的对象。

而且在浏览器中，不存在 Node.js 通过其模块提供的所有不错的 API，例如文件系统访问功能。

另一个很大的不同是，在 Node.js 中，可以控制运行环境。 除非构建的是任何人都可以在任何地方部署的开源应用程序，否则你能知道会在哪个版本的 Node.js 上运行该应用程序。 与浏览器环境（你无法选择访客会使用的浏览器）相比起来，这非常方便。

这意味着可以编写 Node.js 版本支持的所有现代的 ES6-7-8-9 JavaScript。

由于 JavaScript 发展的速度非常快，但是浏览器发展得慢一些，并且用户的升级速度也慢一些，因此有时在 web 上，不得不使用较旧的 JavaScript / ECMAScript 版本。

可以使用 Babel 将代码转换为与 ES5 兼容的代码，再交付给浏览器，但是在 Node.js 中，则不需要这样做。

另一个区别是 Node.js 使用 CommonJS 模块系统，而在浏览器中，则还正在实现 ES 模块标准。

在实践中，这意味着在 Node.js 中使用 `require()`，而在浏览器中则使用 `import`。

[下载](https://nodejs.org/en/)

[文档](http://nodejs.cn/)

### Node常用模块

#### events

events 模块是 Node.js 实现事件驱动的核心,在 node 中大部分的模块的实现都继承了 Events 类。比如 fs 的 readstream,net 的 server 模块。

events 模块只提供了一个对象： events.EventEmitter。EventEmitter 的核心就是事件触发与事件监听器功能的封装,EventEmitter 本质上是一个观察者模式的实现。

所有能触发事件的对象都是 EventEmitter 类的实例。 这些对象有一个 eventEmitter.on() 函数，用于将一个或多个函数绑定到命名事件上。 事件的命名通常是驼峰式的字符串，但也可以使用任何有效的 JavaScript 属性键。

EventEmitter 对象使用 eventEmitter.emit()触发事件,当 EventEmitter 对象触发一个事件时，所有绑定在该事件上的函数都会被同步地调用。 被调用的监听器返回的任何值都将会被忽略并丢弃。

```javascript
const EventEmitter = require('events');

class MyEmitter extends EventEmitter{

}

const myEmitter = new MyEmitter();

myEmitter.on('event', ()=> {
    console.log('is ok~')
});

myEmitter.emit('event');
```

#### path

Node.js 提供了 path 模块,用于处理文件路径和目录路径 . 不同操作系统 表现有所差异 !

##### 获取路径文件名

```javascript
const path = require('path')

path.basename('/path/example/index.js') // index.js
```



##### 获取路径的目录名

```javascript
const path = require('path')

path.dirname('/path/example/index.js') // /path/example
```



##### 获取路径的扩展名

```javascript
const path = require('path')

path.extname('/path/example/index.js') // .js
```



##### 是否是绝对路径

```javascript
const path = require('path')

path.isAbsolute('/path/example/index.js') // true

path.isAbsolute('.') // false
```



##### 拼接路径片段

```javascript
path.join('/path', 'example', './index.js') // /path/example/index.js
```



##### 将路径或路径片段的序列解析为绝对路径

```javascript
path.resolve('/foo/bar', './baz')
// 返回: '/foo/bar/baz'

path.resolve('/foo/bar', '/tmp/file/')
// 返回: '/tmp/file'

path.resolve('wwwroot', 'static_files/png/', '../gif/image.gif')
// 如果当前工作目录是 /home/myself/node，
// 则返回 '/home/myself/node/wwwroot/static_files/gif/image.gif'
```
> 注：如果在处理完所有给定的 `path` 片段之后还未生成绝对路径，则会使用当前工作目录。


##### 规范化路径

```javascript
path.normalize('/path///example/index.js') //  /path/example/index.js
```



##### 解析路径

```javascript
path.parse('/path/example/index.js')

/*
 { 
  root: '/',
  dir: '/path/example',
  base: 'index.js',
  ext: '.js',
  name: 'index' 
  }
*/
```



##### 序列化路径

```javascript
path.format({
  root: '/',
  dir: '/path/example',
  base: 'index.js',
  ext: '.js',
  name: 'index'
}) // /path/example/index.js
```

#### process

process 对象是一个 Global 全局对象，你可以在任何地方使用它，而无需 require。process 是 EventEmitter 的一个实例，所以 process 中也有相关事件的监听。使用 process 对象，可以方便处理进程相关操作。

##### process.arch

为其编译 Node.js 二进制文件的操作系统的 CPU 架构。 可能的值有：`'arm'`、 `'arm64'`、 `'ia32'`、 `'mips'`、 `'mipsel'`、 `'ppc'`、 `'ppc64'`、 `'s390'`、 `'s390x'`、 `'x32'` 和 `'x64'`。

##### process.argv

process.argv 属性会返回一个数组，其中包含当 Node.js 进程被启动时传入的命令行参数。 第一个元素是 [`process.execPath`](http://nodejs.cn/s/MCrAya)。 如果需要访问 `argv[0]` 的原始值，则参见 process.argv0。 第二个元素是正被执行的 JavaScript 文件的路径。 其余的元素是任何额外的命令行参数。

```javascript
node index.js --tips="hello nodejs"

/*
[ '/usr/local/bin/node',
  'xxx/process/index.js',
  '--tips=hello nodejs' ]
*/
```

##### process.argv0

process.argv0 属性保存当 Node.js 启动时传入的 argv[0] 的原始值的只读副本

```javascript
node index.js --tips="hello nodejs" // node
```



##### process.execArgv

process.execArgv 属性返回当 Node.js 进程被启动时，Node.js 特定的命令行选项。 这些选项在 [`process.argv`](http://nodejs.cn/s/wNE2K1) 属性返回的数组中不会出现，并且这些选项中不会包括 Node.js 的可执行脚本名称或者任何在脚本名称后面出现的选项。 这些选项在创建子进程时是有用的，因为他们包含了与父进程一样的执行环境信息。

```javascript
node --harmony index.js --version

console.log(process.execArgv);  // [ '--harmony' ]

console.log(process.argv);

/*
[ '/usr/local/bin/node',
  'xxx/process/index.js',
  '--version' ]
*/
```



##### process.pid

process.pid 属性会返回当前进程的 PID。

```javascript
console.log('process PID: %d', process.pid)

//process PID: 10086
```



##### process.cwd

process.cwd()方法返回进程当前的工作目录

```javascript
console.log(process.cwd()) // E:\learn\node\process
```

##### process.env

process.env 返回当前用户的环境对象



##### process.exit([code])

process.exit()方法终止当前进程，此方法可接收一个退出状态的可选参数 code，不传入时，会返回表示成功的状态码 0。

```javascript
process.on('exit', function(code) {
  console.log('进程退出码是:%d', code) // 进程退出码是:886
})

process.exit(886)
```



##### process.nextTick()

process.nextTick()方法用于延迟回调函数的执行， nextTick 方法会将 callback 中的回调函数延迟到事件循环的下一次循环中，与 setTimeout(fn, 0)相比 nextTick 方法效率高很多，该方法能在任何 I/O 之前调用我们的回调函数。

```javascript
console.log('start')
process.nextTick(() => {
  console.log('nextTick cb')
})
setTimeout(()=> {
    console.log('timeOut')
})
console.log('end')

// start
// end
// nextTick cb
// timeOut
```

