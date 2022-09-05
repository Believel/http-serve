# package.json 参数说明
```js
{
  // ? 指定了模块的主文件是转译后的 lib/http-serve.js
 "main": "lib/http-serve.js",
  // 指定了 CLI 命令可执行文件指向的是转译后的 lib/cli.js
  // 要用这个功能，给package.json中的bin字段一个命令名到文件位置的map。初始化的时候npm会将他链接到prefix/bin（全局初始化）或者./node_modules/.bin/（本地初始化）。
  // 例如：{bin: {"my-name": "./cli.js"}}
  // 如果只有一个可执行文件，并且名字和包名一样，可以按下面来写
  // 发布之后，命令运行：http-serve
  "bin": "lib/cli.js",
  // 指定了发布到 NPM 时包含的文件列表
  "files": ["lib"],
  "scripts": {
    // 使用 tsc 命令可以基于 tsconfig.prod.json 配置来转译 TypeScript 源码
    "build": "tsc -p tsconfig.prod.json",
    // 使用 ts-node 可以直接运行 TypeScript 源码
    "start": "ts-node http-serve/src/cli.ts",
    // 使用 Jest 可以执行所有单测。
    "test": "jest --all"
  },
  "devDependencies": {
    "@types/jest": "^29.0.0",
    // Node.js 内置模块类型声明文件作为开发依赖安装
    "@types/node": "^18.7.14",
    "jest": "^24.9.0",
    "ts-jest": "^24.3.0",
    "ts-node": "^10.9.1",
    "typescript": "^4.8.2"
  },
  "dependencies": {
    // CLI 需要用到的 commander
    "commander": "^9.4.0",
    // 用来处理静态文件请求的
    "ecstatic": "^4.1.4"
  }
}
```

# 发布包
1. 登录npm账号：`npm login`
2. 发布包：`npm publish`
3. 再次发布包，需要更改包的版本号，即修改package.json中的`version`值
4. 如果使用了发布CLI命令，那么执行命令就在bin值中，如果是对象，则运行时是 `键值 `;如果是字符串，则运行时是`包名 `,例如本项目中就是`zpp-serve -p 3000`

# 发布包遇到问题
## 1. npm login时遇到
```js
// 镜像文件现在是淘宝的，不被允许登录
npm ERR! 403 403 Forbidden - PUT https://registry.npmmirror.com/-/user/org.couchdb.user:xx - [FORBIDDEN] Public registration is not allowed

// 解决办法：改成 npm 镜像
npm config set registry https://registry.npmjs.org/
```

## 2. npm publish 时遇到
```js
// 包名重复，换一个包名就可以了
403 Forbidden - PUT https://registry.npmjs.org/http-serve - You do not have permission to publish "http-serve".

// 解决办法：
// 更改 package.json 中的 name 值
```
