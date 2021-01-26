# Access-Control-Allow-Origin
前端解决跨域
### vue proxyTable接口跨域请求调试
```html
在Vue-cli项目中的config文件夹下面有三个JS文件, 首先 ,在 index.js中的Dev{  }中做如下配置
proxyTable: {
      '/api': {
        target: "http://www.baidu.com", // API服务所在IP及端口号
        changeOrigin: true, // 如果设置为true,那么本地会虚拟一个服务器接收你的请求并代你发送该请求，这样就不会有跨域问题（只适合开发环境）
        pathRewrite: {
          '^/api': '' // 重写路径
        }
      }
},
然后,配置开发环境 , 即在 dev.env.js中配置
'use strict'
const merge = require('webpack-merge')
const prodEnv = require('./prod.env')
 
module.exports = merge(prodEnv, {
NODE_ENV: '"development"',
BASE_API: '"http://www.baidu.com"' //配置为本地地址才会访问到本地虚拟的服务器，从而通过第1步中代理访问API服务，避免跨域 
})

最后 ,配置生产环境 ,即在prod.env.js中配置
'use strict'
module.exports = {
  NODE_ENV: '"production"',
  BASE_API: '"http://www.baisu.com"' //产品环境
}

最后,最最最重要 的一点, 一定要重新启动项目 npm run dev , 才会起作用呐 !
```
