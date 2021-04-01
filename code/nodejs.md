基于Google的V8引擎， JavaScript服务端运行环境，事件驱动I/O [文档](https://nodejs.org/dist/latest-v14.x/docs/api/) [代码](https://github.com/nodejs/node) 

NPM 包管理工具

PM2 过程管理工具，用于监视项目，管理进程，pm2自己需要启动一个node服务

nodejs 单线程运行js代码，底层有封装线程池。每个进程启动独立的node服务，可以通过pm2方便管理

**模块解析策略**

nodejs提供的模块，**原生模块**，**核心模块**。在nodejs源代码编译的时候就会被编译成二进制文件，nodejs启动时，这些核心模块就会直接被加载进内存，所以核心模块加载时，相对于文件模块，核心模块引用时不需要进行文件定位和动态编译，速度上有一定的优势。

用户编写的模块，**文件模块**。又分为 自定义模块，通常以包的形式存在，例如npm上的包；以路径形式引入的模块，通常是用户自己编写封装的模块。引入时都是运行时动态加载的，同时由于动态加载，引入时需要进行路径分析，文件定位，动态编译等操作。

自定义模块：

路径分析

1. 查找当前目录下的node_modules目录，看是否有匹配项，如有，命中文件
2. 寻找父目录的下的node_modules，如有，命中文件
3. 按照这个规则一直往父目录搜索直到到根目录下的node_modules

文件定位

当前路径命中的不是一个文件，而是一个目录：

1. 首先会在命中的目录下寻找package.json这个文件并用JSON.parse进行解析，取出json文件中main属性的值，作为命中的文件
2. 如果找不到package.json或者对应的main属性，那么会用这个目录下面index文件作为命中文件，依旧是按照.js，.node，.json这个顺序逐个进行尝试
3. 如果依旧找不到index，那么此次文件定位失败，将会按照上面提到的路径遍历规则，往上一级继续寻找

```javascript
/*文件/root/src/moduleA.js 模块解析*/
var x = require("moduleB")

/* 查找策略
/root/src/node_modules/moduleB.js
/root/src/node_modules/moduleB/package.json (if it specifies a "main" property)
/root/src/node_modules/moduleB/index.js

/root/node_modules/moduleB.js
/root/node_modules/moduleB/package.json (if it specifies a "main" property)
/root/node_modules/moduleB/index.js

/node_modules/moduleB.js
/node_modules/moduleB/package.json (if it specifies a "main" property)
/node_modules/moduleB/index.js
*/
```

**加载顺序**：缓存>核心模块>文件模块

nodejs对于模块加载做了一定程度的优化，所有的文件只要引用过一次，就会被缓存起来，下一次引用时，会先检查缓存中有没有对应的文件，优先从缓存中进行加载，已减少二次开销。但不同于浏览器的缓存，nodejs缓存的是经过分析和编译后的对象，不管是文件模块还是核心模块，二者引用前都会先检查缓存，但核心模块的缓存检查要比文件模块的缓存检查优先。


