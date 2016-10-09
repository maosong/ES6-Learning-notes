# 开始

## 安装nvm和node

```
# 安装nvm
$ curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.32.0/install.sh | bash

# 激活nvm
$ source ~/.nvm/nvm.sh

# 安装最新版Node
$ nvm install node

# 切换到最新版版本
$ nvm use node

# 查看当前Node所有已经实现的ES6特性
$ node --v8-options | grep harmony
```

## 创建项目

```
# 创建项目文件夹
$ mkdir es6-01
$ cd es6-01

# 命令行转码工具
$ npm install --save-dev babel-cli

# 安装polyfill
$ npm install --save-dev babel-polyfill

# ES2015转码规则
$ npm install --save-dev babel-preset-es2015

# react转码规则
$ npm install --save-dev babel-preset-react

# ES7 Candidate（征求意见阶段）语法提案的转码规则
$ npm install --save-dev babel-preset-stage-2
```

```
# 创建Babel配置文件
$ vi .babelrc
{
  "presets": [
    "es2015",
    "react",
    "stage-2"
  ],
  "plugins": []
}
```

```
# 创建package.json配置文件
$ vi package.json
{
  "devDependencies": {
    "babel-cli": "^6.0.0"
  },
  "scripts": {
    "build": "babel src -d lib -s"
  }
}
```

```
# 创建演示代码
$ mkdir -p src lib
$ vi src/example.js
function cook(dessert, ...drink) {
  let temp = dessert;
  for (let i = 0; i < drink.length; ++i) {
    temp += ',' + drink[i];
  }
  console.log(temp);
}
cook('cake', 'juice', 'cola');
```

## 编译项目

```
# 编译
$ babel src/example.js -o lib/example.js -s
or
$ babel src -d lib -s
or
$ npm run build

$ cat lib/example.js
$ cat lib/example.js.map
```
