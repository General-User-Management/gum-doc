# 用法
## 前端接入指南
## 后端接入指南
## 客户端(SDK)使用指南
客户端是除了 API 开放接口之外的接入 GUM 系统的另外一种方式。由官方提供如下几种主流语音SDK，方便用户接入。
### 1.Nodejs SDK
#### 1.quick start
```
const GUM = require('gum-client')

async function run () {
  const gumClient = new GUM()
  gumClient.connect('http://192.168.4.193:3000', {
    healthPath: '/health',
    healthProbe: {
      period: 60,
      timeout: 5
    },
    maxRedirects: 5,
    timeout: 5,
    auto_reconnect: true
  })

  gumClient.on('ready',async () => {
    console.log(`连接成功`)
    const addPolicyResult = await gumClient.addPolicy("测试角色", "/api/v1/mock/status", "(GET)|(POST)")
    console.log(JSON.stringify(addPolicyResult))
  })
}

run()
```
#### 2.option 参数说明
*gumClient.connect(url,option)* 中的 `url/option` 参数说明如下
参数 | 类型 | 是否必填 | 默认值 | 说明 
---|--- |--- |--- |---
url | String | 是 | - | gum-svc 服务 BaseUrl
option | Object | 是 | - | 实例连接 option 选项
option.healthPath | String | 否 | /health | 保持连接健康，检查心跳地址
option.healthProbe | Object | 否 | - | 实例连接 option 选项
option.healthProbe.period | Int | 否 | 60 | 心跳检查周期（秒）
option.healthProbe.timeout | Int | 否 | 5 | 1次检查的超时时间（秒）
option.maxRedirects | Int | 否 | 5 | 最大重连次数
option.timeout | Int | 否 | 5 | 请求超时时间（秒）
option.auto_reconnect | boolean | 否 | true | 是否开启自动重连
#### 3.事件说明
事件名称 | 参数说明 |  备注
--- | --- |--- 
ready | 无参数 | 连接成功后事件
error | 无参数 | 错误事件
### 2.JAVA SDK
### 3.Golang SDK
### 4.Python SDK
## 中间件使用指南  
### 认证中间件使用指南
### 鉴权中间件使用指南 
## GUM实践案例