# 客户端API列表
## 1. 给角色增加一个api权限
<table>
    <tr>
        <td align="center"  bgcolor = "#808000" >说明项</td>
        <td align="center"  bgcolor = "#808000" > 描述</td>
    <tr>
    <tr>
        <td align="left">名字</td>
        <td align="left"> addPolicy</td>
    <tr>
    <tr>
        <td align="left">作用</td>
        <td align="left">给某个角色增加一个API接口的权限</td>
    <tr>
    <tr>
        <td align="left">举例</td>
        <td align="left">给 系统管理员 增加 POST 请求到URL为 /api/v1/mock/status 的权限</td>
    <tr>
    <tr>
        <td align="left">使用</td>
        <td align="left">client.addPolicy("系统管理员", "/api/v1/mock/status", "POST")</td>
    <tr>
</table>

## 2. 批量增加p域
<table>
    <tr>
        <td align="center"  bgcolor = "#808000" >说明项</td>
        <td align="center"  bgcolor = "#808000" > 描述</td>
    <tr>
    <tr>
        <td align="left">名字</td>
        <td align="left"> addPolicies</td>
    <tr>
    <tr>
        <td align="left">作用</td>
        <td align="left">批量给多个不同角色赋予不同权限</td>
    <tr>
    <tr>
        <td align="left">举例</td>
        <td align="left">1.给系统管理员1增加GET、POST、PUT、PATCH、DELETE请求到URL为`api/v1/users`的权限；
        2.给系统管理员2增加GET请求到URL为api/v1/role为前缀的权限；
        3.给系统管理员3增加POST请求到URLapi/v1/school/:schoolid/teacher/:teacherid的RESTful的权限</td>
    <tr>
    <tr>
        <td align="left">使用</td>
        <td align="left">见下面的代码块</td>
    <tr>
</table>
```
client.addPolicies([
                [
                    "系统管理员1",
                    "api/v1/users",
                    "(GET)|(POST)|(PUT)|(PATCH)|(DELETE)"
                ],
                [
                    "机构管理员2",
                    "api/v1/role/*",
                    "GET"
                ],
                [
                    "机构管理员3",
                    "api/v1/school/:schoolid/teacher/:teacherid",
                    "POST"
                ]
            ])
```


## 3. 给用户赋予某个角色
<table>
    <tr>
        <td align="center"  bgcolor = "#808000" >说明项</td>
        <td align="center"  bgcolor = "#808000" > 描述</td>
    <tr>
    <tr>
        <td align="left">名字</td>
        <td align="left">addRoleForUser</td>
    <tr>
    <tr>
        <td align="left">作用</td>
        <td align="left">给某个用户赋予某个角色（某个角色里面增加某个用户）</td>
    <tr>
    <tr>
        <td align="left">举例</td>
        <td align="left">给zhangsan这个用户赋予为管理员这个角色</td>
    <tr>
    <tr>
        <td align="left">使用</td>
        <td align="left">client.addRoleForUser("zhangsan", "管理员")</td>
    <tr>
</table>
## 4. 获取到用户拥有的权限
## 5. 获取角色拥有的权限
## 6. 获取用户拥有的角色
## 7. 获取角色拥有的用户
## 8. 获取所有的实体
## 9. 获取所有的资源列表
## 10. 获取所有的行为
## 11. 获取所有的角色
## 12. 获取所有的策略列表
## 13. 查询用户分配给了那些角色
## 14. 批量移除角色权限
## 15. 移除某个用户有用的某个角色
