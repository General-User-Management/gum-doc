# 客户端API列表
<style>
table, th, td {
  border: 1px solid black;
  border-collapse: collapse;
}
.title {
  font-size: 100%;
  font-weight: bold;
}
</style>
## 1. 给角色增加一个api权限
<table>
    <tr class="title">
        <td align="center"  bgcolor = "#C0C0C0" >说明项</td>
        <td align="center"  bgcolor = "#C0C0C0" > 描述</td>
    <tr>
    <tr>
        <td align="left">名字</td>
        <td align="left" style="font-weight: bold"> addPolicy</td>
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
    <tr class="title">
        <td align="center"  bgcolor = "#C0C0C0" >说明项</td>
        <td align="center"  bgcolor = "#C0C0C0" > 描述</td>
    <tr>
    <tr>
        <td align="left">名字</td>
        <td align="left" style="font-weight: bold"> addPolicies</td>
    <tr>
    <tr>
        <td align="left">作用</td>
        <td align="left">批量给多个不同角色赋予不同权限</td>
    <tr>
    <tr>
        <td align="left">举例</td>
        <td align="left">1.给<nobr style="font-weight: bold">系统管理员1</nobr>增加 GET、POST、PUT、PATCH、DELETE 请求到URL为`api/v1/users`的权限；<br>
        2.给<nobr style="font-weight: bold">系统管理员2</nobr>增加 GET 请求到 URL 为 api/v1/role 为前缀的权限；<br>
        3.给<nobr style="font-weight: bold">系统管理员3</nobr>增加 POST 请求到URL 为 api/v1/school/:schoolid/teacher/:teacherid 的 RESTful 的权限</td>
    <tr>
    <tr>
        <td align="left">使用</td>
        <td align="left">见下面的代码块</td>
    <tr>
</table>

```js
client.addPolicies([
                [
                    "系统管理员1",
                    "api/v1/users",
                    "(GET)|(POST)|(PUT)|(PATCH)|(DELETE)"
                ],
                [
                    "系统管理员2",
                    "api/v1/role/*",
                    "GET"
                ],
                [
                    "系统管理员3",
                    "api/v1/school/:schoolid/teacher/:teacherid",
                    "POST"
                ]
            ])
```

## 3. 给用户赋予某个角色
<table>
    <tr class="title">
        <td align="center"  bgcolor = "#C0C0C0" >说明项</td>
        <td align="center"  bgcolor = "#C0C0C0" > 描述</td>
    <tr>
    <tr>
        <td align="left">名字</td>
        <td align="left" style="font-weight: bold">addRoleForUser</td>
    <tr>
    <tr>
        <td align="left">作用</td>
        <td align="left">给某个用户赋予某个角色（某个角色里面增加某个用户）</td>
    <tr>
    <tr>
        <td align="left">举例</td>
        <td align="left">给<nobr style="font-weight: bold">zhangsan</nobr>这个用户赋予为管理员这个角色</td>
    <tr>
    <tr>
        <td align="left">使用</td>
        <td align="left">client.addRoleForUser("zhangsan", "管理员")</td>
    <tr>
</table>

## 4. 获取到用户拥有的权限
<table>
    <tr class="title">
        <td align="center"  bgcolor = "#C0C0C0" >说明项</td>
        <td align="center"  bgcolor = "#C0C0C0" > 描述</td>
    <tr>
    <tr>
        <td align="left">名字</td>
        <td align="left" style="font-weight: bold">getImplicitPermissionsForUser</td>
    <tr>
    <tr>
        <td align="left">作用</td>
        <td align="left">获取某个用户拥有的所有角色的所有权限列表</td>
    <tr>
    <tr>
        <td align="left">举例</td>
        <td align="left">获取<nobr style="font-weight: bold">hyx</nobr>这个用户所有API访问权限（包括提供API权限的角色）</td>
    <tr>
    <tr>
        <td align="left">使用</td>
        <td align="left">client.getImplicitPermissionsForUser("hyx")</td>
    <tr>
    <tr>
        <td align="left">返回示例</td>
        <td align="left">见下面所示(data字段)</td>
    <tr>
</table>
```json
{
    "code": 0,
    "data": [
        [
            "机构管理员",
            "/api/v1/check",
            "POST"
        ],
        [
            "系统管理员1",
            "api/v1/users",
            "(GET)|(POST)|(PUT)|(PATCH)|(DELETE)"
        ],
        [
            "系统管理员1",
            "/api/v1/mock/status",
            "DELETE"
        ]
    ]
}
```

## 5. 获取角色拥有的权限
<table>
    <tr class="title">
        <td align="center"  bgcolor = "#C0C0C0" >说明项</td>
        <td align="center"  bgcolor = "#C0C0C0" > 描述</td>
    <tr>
    <tr>
        <td align="left">名字</td>
        <td align="left" style="font-weight: bold">getFilteredNamedPolicy</td>
    <tr>
    <tr>
        <td align="left">作用</td>
        <td align="left">获取某个角色的所有权限列表</td>
    <tr>
    <tr>
        <td align="left">举例</td>
        <td align="left">获取<nobr style="font-weight: bold">系统管理员1</nobr>这个角色所有API访问权限</td>
    <tr>
    <tr>
        <td align="left">使用</td>
        <td align="left">client.getFilteredNamedPolicy("系统管理员1")</td>
    <tr>
    <tr>
        <td align="left">返回示例</td>
        <td align="left">见下面所示(data字段)</td>
    <tr>
</table>
```json
{
    "code": 0,
    "data": [
        [
            "系统管理员1",
            "api/v1/users",
            "(GET)|(POST)|(PUT)|(PATCH)|(DELETE)"
        ],
        [
            "系统管理员1",
            "/api/v1/mock/status",
            "DELETE"
        ]
    ]
}
```

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
