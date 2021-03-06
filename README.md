# puer-mock

[![NPM version][npm-image]][npm-url]

[npm-image]: https://img.shields.io/npm/v/puer-mock.svg?style=flat-square
[npm-url]: https://npmjs.org/package/puer-mock

[Puer](https://github.com/leeluolee/puer) + [Mock.js](https://github.com/nuysoft/Mock) = A Configurable mock server with configurable mock(random) data.

Start a mock server never ever so easy and configurable, no code needed, you only need config some mock api route and some mock data template, it all done! 

## features

* effective immediately when config changed
* JSONP support
* CORS support
* built-in API doc

## install

Please install [puer](https://github.com/leeluolee/puer) first.

> Puer - more than a live-reload server , built for efficient frontend development

```
npm install puer-mock
```

## usage

1. copy `node_modules/puer-mock/example` files to your project root directory
2. cd `your project root`
3. `puer -a _mockserver.js`
4. view mock api
  * open `http://localhost:8000/api/users` view mock api return mock data
  * open `http://localhost:8000/api/users?callback=test` view mock api return mock data by JSONP
  * open `http://localhost:8000/_apidoc` view built-in all mock api doc
5. define your mock api in `_mockserver.json`
6. view your mock api(Yes! it with immediate effect)

## config

The minimal `_mockserver.json`

```json
{
    "api": {
        "GET /api/users": {
            "response": {}
        }
    }
}
```

You can see more settings to config mock server in [`_mockserver.json`](https://github.com/ufologist/puer-mock/blob/master/example/_mockserver.json).

* comment is nice
* config route and mock response data template is so easy
* more data template please see [Mock.js examples](http://mockjs.com/examples.html)
* disable a route is convenient
* mock server will effective immediately when you changed `_mockserver.json`

## customize

* You may customize `/_apidoc` route service a more graceful doc.

  ```javascript
  // _mockserver.js
  module.exports = require('puer-mock')(null, null, function(mockConfig) {
      // 任你自由发挥
      return '<pre>' + JSON.stringify(mockConfig, null, 4) + '</pre>';
  });
  ```

* Play it fun with your imagination.

  ```javascript
  // _mockserver.js
  var puerMock = require('puer-mock');
  var routeConfig = puerMock();
  // 其实你完全可以这样来玩, 在这里接着定义 route 即可, 发挥你的想象力
  // 例如定义一个常用的 500 接口, 来测试服务器报错的情况
  routeConfig['GET /500'] = function(request, response, next) {
      response.status(500).end();
  };
  module.exports = routeConfig;
  ```

## example

眼见为实耳听为虚, puer-mock 让你一秒钟就能拥有一个强大的 mock server, 所以请不要再自己手工做假数据了, 赶快尝试一下让你的工作效率翻番吧!

### 配置 API 并生成随机数据
![puer-mock-example](https://ufologist.github.io/puer-mock/puer-mock-example.png)

### 查看所有的 API 接口文档
![puer-mock-api-doc](https://ufologist.github.io/puer-mock/puer-mock-api-doc.png?v1)

## one more thing

谁需要这个工具
* 前端/APP端
* 任何与后端接口打交道的人
* [为什么你需要一个 mock server](https://github.com/ufologist/puer-mock/blob/master/why-your-need-a-mock-server.md)

感谢 puer 提供了如此强大的 mock 机制, 感谢 Mock.js 带来的假数据, 我才有幸做了这么一个扩展工具.