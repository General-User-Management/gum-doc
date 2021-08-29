# 特性

- **权限控制功能强大**  
提供前端响应式权限策略执行，同时提供后端API接口认证和鉴权，其为了方便用户使用，提供中间件组件形式；
- **使用成本低**  
接入成本非常低，几乎可以忽略不计。前端可以通过引入Vue组件使用。后端可以使用 middleware 中间件使用； 
- **嵌入目标系统耦合度低**  
由于接入方式的灵活便捷，因此使得对目标系统几乎零侵入。通过组件或者中间件的方式引用即可
- **部署简单**  
只需要部署系统各微服务代码即可，且只依赖了 mongo 和 redis(非必须，如目标系统体量不大，无需观察者，可以不用)