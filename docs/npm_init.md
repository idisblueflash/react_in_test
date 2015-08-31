# npm初始化

进入目录myAppWithTest，运行npm初始化命令：

```
cd myAppWithTest
npm init
``` 
在对话环境中，填写项目配置：

```
This utility will walk you through creating a package.json file.
It only covers the most common items, and tries to guess sensible defaults.

See `npm help json` for definitive documentation on these fields
and exactly what they do.

Use `npm install <pkg> --save` afterwards to install a package and
save it as a dependency in the package.json file.

Press ^C at any time to quit.
name: (myAppWithTest) my-app-with-test  // 输入项目名称
version: (1.0.0) // 回车，使用默认版本号
description: test env for react // 输入项目描述
entry point: (index.js) // 回车，使用默认文件名（文件不存在，需要单独创建）
test command: 	// 回车，使用默认值
git repository: // 回车留空或填入Git地址
keywords: react test // 填写关键字react和test
author: idisblueflash@gmail.com // 填写作者邮箱
license: (ISC) // 回车，使用默认值
```
系统会生成相应的配置文件

```
About to write to /Users/fox/Documents/react_in_test/sources/npm_init/myAppWithTest/package.json:

{
  "name": "my-app-with-test",
  "version": "1.0.0",
  "description": "test env for react",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "keywords": [
    "react",
    "test"
  ],
  "author": "idisblueflash@gmail.com",
  "license": "ISC"
}


Is this ok? (yes)  // 回车确认
```

npm会把配置存在package.json里。