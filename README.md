# 配置环境变量实现 指令 运行 打包 不同后台地址

## 指令详解

  ```bash
    "scripts": {
      "start": "dotenv -e .env.test react-app-rewired start",
      "start--test": "dotenv -e .env.test react-app-rewired start",
      "start--dev": "dotenv -e .env.dev react-app-rewired start",
      "start--prod": "dotenv -e .env.prod react-app-rewired start",
      "build": "dotenv -e .env.prod react-app-rewired build",
      "build--test": "dotenv -e .env.test react-app-rewired build",
      "build--prod": "dotenv -e .env.prod react-app-rewired build",
      "test": "react-app-rewired test",
      "eject": "react-app-rewired eject"
    }
  ```

## 实现步骤

  1.初始化项目

  ```bash
    yarn global add react-create-app
    #OR
    npm install react-create-app -g
    # then
    yarn create react-app my-app
    cd my-app
    yarn start
  ```

  2.在项目根目录创建 **.env, .env.test, .env.prod** 文件内容类似

  ```bash
    # .env.test 其他文件相同
    # react的环境变量最好是用 REACT_ 开头
    REACT_APP_BASE_URL = '测试url'
  ```

  3.使用 **react-app-rewired，customize-cra**
    备注： react-app-rewired，customize-cra 简单来讲就是用来覆盖或者替换 react-create-app 默认配置， 而 config-overrides.js文件 是用来更改或者替换 react-app-rewired 默认配置的

  ```bash
    yarn add react-app-rewired customize-cra
  ```

  4.全局使用 **dotenv-cli**， 使用说明：<https://github.com/entropitor/dotenv-cli>

  ```bash
    yarn global add dotenv-cli
  ```

  5.在项目根目录创建 **config-overrides.js** 文件内容如下, 使用Antd时候也会用到

  ```bash
    module.exports = function override(config, env) {
      // do stuff with the webpack config...
      return config
    }
  ```

  6.指令说明

  ```bash
    # start
    yarn start
    yarn start--test
    yarn start--dev
    yarn start--prod

    # build
    yarn build
    yarn build--test
    yarn build--prod
  ```

  7.修改项目的 **api的入口url**, 就能根据不同的环境变量的值来作为不同的后台请求地址了

  ```bash
    // const BASE  = 'http://123.123.123:8080'
    const BASE = 'process.env.REACT_APP_BASE_URL'
  ```
