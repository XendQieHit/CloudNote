下载安装node.js（(https://nodejs.org/)）

在cmd中 配置国内镜像npm，以提高下载速度
```Shell
$ npm install -g cnpm --registry=https://registry.npmmirror.com
```

之后就可以在cmd中直接使用cnpm指令来安包了（PowerShell不行！！！）

附：通过cmd命令行切换所在目录
```Shell
D:\ #换盘
cd 你的项目文件路径
```

### 之后的操作都在本地项目文件夹（也就是getStartMC文件夹）里进行，包括新建文件之类的

打开cmd，安装库
```Shell
cnpm install express #安装服务端基础包
cnpm install nodemon #安装这个之后就可以动态修改网页内容并实时更新了
```

新建一个js文件，里面内容如下
```JavaScript
// server.js
const express = require('express');
const path = require('path');

const app = express();
const PORT = 3000;

// 设置静态文件目录
app.use(express.static(path.join(__dirname)));

// 处理根路径请求
app.get('/', (req, res) => {
    res.sendFile(path.join(__dirname, 'index.html'));
});

// 启动服务器
app.listen(PORT, () => {
    console.log(`Server is running on http://localhost:${PORT}`);
});
```

在cmd中运行命令
```Shell
node 刚刚写的文件.js
nodemon 刚刚写的文件.js #如果安装了nodemon就用这个指令
```

如果没有什么错误信息出来的话就是成功了

这个是没安装库的情况
```Shell
node:internal/modules/cjs/loader:1228
	throw err;
	^
	
Error: Cannot find module 'express'
Require stack:
- 你的运行脚本的路径.js
	at Module._resolveFilename (node:internal/modules/cjs/loader:1225:15)
	at Module._load (node:internal/modules/cjs/loader:1051:27
	at Module.require (node:internal/modules/cjs/loader:1311:19)
	at require (node:internal/modules/helpers:179:18) at Object.<anonymous> (你的运行脚本的路径.js:2:17)
	at Module._compile (node:internal/modules/cjs/loader:1469:14)
	at Module._extensions..js (node:internal/modules/cjs/loader:1548:10)
	at Module.load (node:internal/modules/cjs/loader:1288:32)
	at Module._load (node:internal/modules/cjs/loader:1104:12)
	at Function.executeUserEntryPoint [as runMain] (node:internal/modules/run_main:174:12) { code: 'MODULE_NOT_FOUND', requireStack: [ '你的运行脚本的路径.js' ] }
```

如果你觉得这样手动反复打开cmd麻烦，你可以直接新建个bat文件，里面内容就是上面的启动指令

git commit时，不想上传这些node.js文件的话，要在本地项目文件里新建一个 .gitignore

新建完一个 .gitignore文件之后，直接打开进行编辑
### 示例 `.gitignore` 文件

以下是一个常见的 `.gitignore` 文件示例，适用于 Node.js 项目：

```gitignore
# 忽略server.js文件
server.js
package.josn

# 忽略 node_modules 目录
node_modules/

# 忽略所有 .log 文件
*.log

# 忽略所有 .env 文件
.env

# 忽略所有临时文件
*.tmp

# 忽略所有编译输出
dist/
build/

# 忽略 IDE 或编辑器生成的文件
.vscode/
.idea/
*.swp
*.swo
*.swn
```

所有文件弄好后，里面的文件目录差不多就是这样
![[Pasted image 20241013143048.png]]