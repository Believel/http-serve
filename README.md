# packages

```js
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
```

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
}
```


待办： 成功发布一个npm包，并使用它