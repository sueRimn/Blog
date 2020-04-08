## 安装Mongodb和可视化工具Studio 3T

`Mongodb`和`Studio 3T`官网下载后安装。具体可谷歌或百度。然后启动`Mongodb`。

然后打开`Studio 3T`，连接数据库端口，右键新建一个数据库，我这里新建的数据库为`login`。

![1573117983384](C:\Users\16583\Desktop\cut\1573117983384.png)

`user`是自己新建的数据集合，大概如下：

![1573118019894](C:\Users\16583\Desktop\cut\1573118019894.png)

##  搭建服务器

我的项目是`Vue cli 3 + Electron + express`的，在项目的根目录新建一个文件夹`service`，然后在该文件夹下新建几个文件夹分别是`database`、`routes`以及一个服务器启动文件`server.js`，具体如下 

```JavaScript
├─ service
│    ├─ database
│    ├─ routes
│    └─ server.js
├─ src
│    ├─ App.vue
│    ├─ assets
│    ├─ background.js
│    ├─ common
│    ├─ components
│    ├─ main.js
│    ├─ router.js
│    ├─ store.js
│    └─ views
└─ vue.config.js
```

### 1、搭建服务器

安装`express`：

```bash
npm add express -S
```

在`server.js`文件中写入：

```javascript
const express = require('express')
const app = express()

// 请求头设置，以防万一
app.all('*', (req, res, next) => {
  res.header('Access-Control-Allow-Origin', '*')
  res.header('Access-Control-Allow-Headers', 'X-Requested-With,Content-Type')
  res.header('Access-Control-Allow-Methods', 'PUT,POST,GET,DELETE,OPTIONS')
  res.header('X-Powered-By', ' 3.2.1')
  res.header('Content-Type', 'application/json;charset=utf-8')
  return next()
})
app.get('/', (req, res) => res.send('hello from server'))
app.listen(3000, () => console.log('app listening on port 3000'))

```

在`service`路径下启动服务输入`node server.js`，简单服务器搭建成功。

为了解决跨域问题，需要在`vue.config.js`文件中加入：

```javascript
devServer: {
    port: 8080,
    proxy: {
      '/user': {
        target: 'http://127.0.0.1:3000',
        changeOrigin: true // 跨域
      }
    }
  },
```

### 2、连接数据库

安装依赖：

```bash
npm add mongodb mongoose -S
```

在`database`文件夹下新建文件`db.js`，然后输入：

```javascript
const mongoose = require('mongoose')
const DBURL = 'mongodb://localhost:27017/login' //login 就是自己创建的数据库名

// 连接数据库
mongoose.connect(DBURL)

// 连接成功
mongoose.connection.on('connected', () => {
  console.log('mongoose connection open to ' + DBURL)
})

// 连接失败
mongoose.connection.on('error', error => {
  console.log('Mongoose connection error:' + error)
})

// 连接断开
mongoose.connection.on('disconnected', function () {
  console.log('Mongoose connection disconnected')
})
module.exports = mongoose

```

然后再新建一个文件`user.js`创建数据库`Schema`，即数据库集合的模型骨架，或者是数据属性模型传统意义的表结构。

```javascript
/*
 定义一个user的Schema
*/
const mongoose = require('./db.js')
const Schema = mongoose.Schema

// 创建一个模型
const UserSchema = new Schema({
  username: String,
  password: String
})

// 导出model模块
module.exports = mongoose.model('User', UserSchema)

```

### 3、编写接口，路由模块化

为了方便管理，这里需要使用到`express`的路由中间件。

为了方便对前端发送过来的数据进行解析，引用一个`body-parser`中间件，安装：

```bash
npm add body-parser -S
```

然后在`server.js`中引入：

```javascript
const bodyParser = require('body-parser')
app.use(bodyParser.json())
app.use(bodyParser.urlencoded({ extended: false }))
```

在`routes`文件夹中新建文件`user.js`：

```javascript
const express = require('express')
const router = express.Router()
const User = require('../database/user')

router.post('/login', async (req, res, next) => {
  console.log(req.body)
//这里的req.body 其实使用了body-parser中间件 用来对前端发送来的数据进行解析
  const username = req.body.username
  const password = req.body.password
  // 判断用户名和密码是否和数据库的相同
  let doc = await User.findOne({ username })
  if (!doc) {
    req.body = {
      code: -1,
      msg: '用户名不存在'
    }
    res.send(req.body)
  } else if (doc.password !== password) {
    req.body = {
      code: -1,
      msg: '密码错误'
    }
    res.send(req.body)
  } else if (doc.password === password) {
    try {
      req.body = {
        code: 0,
        msg: '登录成功',
        username
      }
      res.send(req.body)
    } catch (err) {
      req.body = {
        code: -1,
        msg: '登录失败，请重新登录'
      }
      res.send(req.body)
    }
  }
    module.exports = router

```

然后在`server.js`中引入路由：

```javascript
const user = require('./router/user')
app.use('/user', user)
```

## 完善登录功能

安装`axios`:

```bash
npm add axios -S
```

将`axios`改写成`Vue`的原型属性：

```javascript
// main.js
import axios from 'axios'
Vue.prototype.$ajax = axios
```

打开登录页面`SignIn.vue`，调用接口:

```javascript
methods: {
    handleSubmit (e) {
      e.preventDefault()
      this.form.validateFields((err, values) => {
        if (!err) {
          console.log('Received values of form: ', values)
          let loginParams = {
            username: values.userName,
            password: values.password
          }
          this.$ajax.post('/user/login', loginParams).then(res => {
            let result = res.data

            if (result.code === 0) {
              setTimeout(() => {
                this.spinning = true
                const msg = result.msg || '登录成功'
                this.$message.success(msg)
                sessionStorage.setItem('user', JSON.stringify(result.username))
                this.$router.push('/')// 登录后转向主页
              }, 1000)
              this.spinning = false
            } else {
              const errorMsg = result.errorMsg || '登录失败'
              this.$message.warn(errorMsg)
            }
          }).catch(err => {
            console.log(err)
          })
        }
      })
    }
  }
```



