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
.illustrate {
  width: 10%
}
.describe {
  width: 90%
}
</style>
## 1. 给角色增加一个api权限
<table>
    <tr class="title">
        <td align="center"  bgcolor = "#C0C0C0" class="illustrate">说明项</td>
        <td align="center"  bgcolor = "#C0C0C0" class="describe"> 描述</td>
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
    <tr>
        <td align="left">返回说明</td>
        <td align="left">true: 操作成功<br>false:操作失败</td>
    <tr>
</table>
<br>

## 2. 批量增加p域
<table>
    <tr class="title">
        <td align="center"  bgcolor = "#C0C0C0" class="illustrate">说明项</td>
        <td align="center"  bgcolor = "#C0C0C0" class="describe"> 描述</td>
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
    <tr>
        <td align="left">返回说明</td>
        <td align="left">true: 操作成功<br>false:操作失败</td>
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
        <td align="center"  bgcolor = "#C0C0C0" class="illustrate">说明项</td>
        <td align="center"  bgcolor = "#C0C0C0" class="describe"> 描述</td>
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
    <tr>
        <td align="left">返回说明</td>
        <td align="left">true: 操作成功<br>false:操作失败</td>
    <tr>
</table>
<br>

## 4. 获取到用户拥有的权限
<table>
    <tr class="title">
        <td align="center"  bgcolor = "#C0C0C0" class="illustrate">说明项</td>
        <td align="center"  bgcolor = "#C0C0C0" class="describe"> 描述</td>
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
        <td align="left">返回</td>
        <td align="left">见下面代码块所示</td>
    <tr>
</table>

```json
[
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
```

## 5. 获取角色拥有的权限
<table>
    <tr class="title">
        <td align="center"  bgcolor = "#C0C0C0" class="illustrate">说明项</td>
        <td align="center"  bgcolor = "#C0C0C0" class="describe"> 描述</td>
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
        <td align="left">返回</td>
        <td align="left">见下面代码块所示</td>
    <tr>
</table>

```json
[
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
```

## 6. 获取用户拥有的角色
<table>
    <tr class="title">
        <td align="center"  bgcolor = "#C0C0C0" class="illustrate">说明项</td>
        <td align="center"  bgcolor = "#C0C0C0" class="describe"> 描述</td>
    <tr>
    <tr>
        <td align="left">名字</td>
        <td align="left" style="font-weight: bold">getImplicitRolesForUser / getRolesForUser</td>
    <tr>
    <tr>
        <td align="left">作用</td>
        <td align="left">获取某个用户所拥有的角色列表</td>
    <tr>
    <tr>
        <td align="left">举例</td>
        <td align="left">获取<nobr style="font-weight: bold">hyx</nobr>这个用户拥有的角色列表</td>
    <tr>
    <tr>
        <td align="left">使用</td>
        <td align="left">client.getImplicitRolesForUser("hyx") 或者<br>client.getRolesForUser("hyx")</td>
    <tr>
    <tr>
        <td align="left">返回</td>
        <td align="left">见下面代码块所示</td>
    <tr>
</table>

```json
[
    "机构管理员",
    "系统管理员1"
]
```

## 7. 获取角色拥有的用户
<table>
    <tr class="title">
        <td align="center"  bgcolor = "#C0C0C0" class="illustrate">说明项</td>
        <td align="center"  bgcolor = "#C0C0C0" class="describe"> 描述</td>
    <tr>
    <tr>
        <td align="left">名字</td>
        <td align="left" style="font-weight: bold">getUsersForRole</td>
    <tr>
    <tr>
        <td align="left">作用</td>
        <td align="left">获取某个角色所拥有的用户列表</td>
    <tr>
    <tr>
        <td align="left">举例</td>
        <td align="left">获取<nobr style="font-weight: bold">机构管理员</nobr>这个角色拥有的用户列表</td>
    <tr>
    <tr>
        <td align="left">使用</td>
        <td align="left">client.getUsersForRole("机构管理员")</td>
    <tr>
    <tr>
        <td align="left">返回</td>
        <td align="left">见下面代码块所示</td>
    <tr>
</table>

```json
["hyx","ypj"]
```

## 8. 获取所有的实体(角色)
<table>
    <tr class="title">
        <td align="center"  bgcolor = "#C0C0C0" class="illustrate">说明项</td>
        <td align="center"  bgcolor = "#C0C0C0" class="describe"> 描述</td>
    <tr>
    <tr>
        <td align="left">名字</td>
        <td align="left" style="font-weight: bold">getAllSubjects</td>
    <tr>
    <tr>
        <td align="left">作用</td>
        <td align="left">获取系统中所有的角色</td>
    <tr>
    <tr>
        <td align="left">举例</td>
        <td align="left">获取系统中的角色列表</td>
    <tr>
    <tr>
        <td align="left">使用</td>
        <td align="left">client.getAllSubjects()</td>
    <tr>
    <tr>
        <td align="left">返回</td>
        <td align="left">见下面代码块所示</td>
    <tr>
</table>

```json
[
    "机构管理员",
    "系统管理员1",
    "机构管理员2",
    "机构管理员3"
]
```
## 9. 获取所有的资源（API）列表
<table>
    <tr class="title">
        <td align="center"  bgcolor = "#C0C0C0" class="illustrate">说明项</td>
        <td align="center"  bgcolor = "#C0C0C0" class="describe"> 描述</td>
    <tr>
    <tr>
        <td align="left">名字</td>
        <td align="left" style="font-weight: bold">getAllObjects</td>
    <tr>
    <tr>
        <td align="left">作用</td>
        <td align="left">获取系统中所有的API</td>
    <tr>
    <tr>
        <td align="left">举例</td>
        <td align="left">获取系统中的API列表</td>
    <tr>
    <tr>
        <td align="left">使用</td>
        <td align="left">client.getAllObjects()</td>
    <tr>
    <tr>
        <td align="left">返回</td>
        <td align="left">见下面代码块所示</td>
    <tr>
</table>

```json
[
    "/api/v1/check",
    "api/v1/users",
    "api/v1/role/*",
    "api/v1/school/:schoolid/teacher/:teacherid",
    "/api/v1/mock/status"
]
```

## 10. 获取所有的行为（方法method）
<table>
    <tr class="title">
        <td align="center"  bgcolor = "#C0C0C0" class="illustrate">说明项</td>
        <td align="center"  bgcolor = "#C0C0C0" class="describe"> 描述</td>
    <tr>
    <tr>
        <td align="left">名字</td>
        <td align="left" style="font-weight: bold">getAllActions</td>
    <tr>
    <tr>
        <td align="left">作用</td>
        <td align="left">获取系统中所有的 method</td>
    <tr>
    <tr>
        <td align="left">举例</td>
        <td align="left">获取系统中的 method 列表</td>
    <tr>
    <tr>
        <td align="left">使用</td>
        <td align="left">client.getAllActions()</td>
    <tr>
    <tr>
        <td align="left">返回</td>
        <td align="left">见下面代码块所示</td>
    <tr>
</table>

```json
[
    "POST",
    "(GET)|(POST)|(PUT)|(PATCH)|(DELETE)",
    "GET",
    "DELETE"
]
```

## 11. 获取所有绑定着用户的角色
<table>
    <tr class="title">
        <td align="center"  bgcolor = "#C0C0C0" class="illustrate">说明项</td>
        <td align="center"  bgcolor = "#C0C0C0" class="describe"> 描述</td>
    <tr>
    <tr>
        <td align="left">名字</td>
        <td align="left" style="font-weight: bold">getAllRoles</td>
    <tr>
    <tr>
        <td align="left">作用</td>
        <td align="left">获取系统中所有存在用户的角色列表；<br>注意它与 getAllSubjects 不一样的地方是:getAllRoles 只会查询到存在用户的角色列表</td>
    <tr>
    <tr>
        <td align="left">举例</td>
        <td align="left">查询存在用户的角色列表</td>
    <tr>
    <tr>
        <td align="left">使用</td>
        <td align="left">client.getAllRoles()</td>
    <tr>
    <tr>
        <td align="left">返回</td>
        <td align="left">见下面代码块所示</td>
    <tr>
</table>

```json
[
    "机构管理员",
    "系统管理员1"
]
```

## 12. 获取所有的策略列表
<table>
    <tr class="title">
        <td align="center"  bgcolor = "#C0C0C0" class="illustrate">说明项</td>
        <td align="center"  bgcolor = "#C0C0C0" class="describe"> 描述</td>
    <tr>
    <tr>
        <td align="left">名字</td>
        <td align="left" style="font-weight: bold">getPolicy</td>
    <tr>
    <tr>
        <td align="left">作用</td>
        <td align="left">获取系统中所有角色的所有API权限</td>
    <tr>
    <tr>
        <td align="left">举例</td>
        <td align="left">查询系统中存在所有角色的所有API权限</td>
    <tr>
    <tr>
        <td align="left">使用</td>
        <td align="left">client.getPolicy()</td>
    <tr>
    <tr>
        <td align="left">返回</td>
        <td align="left">见下面代码块所示</td>
    <tr>
</table>

```json
[
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
        "机构管理员2",
        "api/v1/role/*",
        "GET"
    ],
    [
        "机构管理员3",
        "api/v1/school/:schoolid/teacher/:teacherid",
        "POST"
    ],
    [
        "系统管理员1",
        "/api/v1/mock/status",
        "DELETE"
    ]
]
```
## 13. 查询用户分配给了那些角色
<table>
    <tr class="title">
        <td align="center"  bgcolor = "#C0C0C0" class="illustrate">说明项</td>
        <td align="center"  bgcolor = "#C0C0C0" class="describe"> 描述</td>
    <tr>
    <tr>
        <td align="left">名字</td>
        <td align="left" style="font-weight: bold">getFilteredNamedGroupingPolicy</td>
    <tr>
    <tr>
        <td align="left">作用</td>
        <td align="left">获取某个用户分配存在的角色列表<br>与 getImplicitRolesForUser / getRolesForUser 达到的效果一样，但注意其返回格式有区别</td>
    <tr>
    <tr>
        <td align="left">举例</td>
        <td align="left">查询某个用户分配存在那些角色</td>
    <tr>
    <tr>
        <td align="left">使用</td>
        <td align="left">client.getFilteredNamedGroupingPolicy('hyx')</td>
    <tr>
    <tr>
        <td align="left">返回</td>
        <td align="left">见下面代码块所示</td>
    <tr>
</table>

```json
[
    [
        "hyx",
        "机构管理员"
    ],
    [
        "hyx",
        "系统管理员1"
    ]
]
```
## 14. 批量移除角色权限
<table>
    <tr class="title">
        <td align="center"  bgcolor = "#C0C0C0" class="illustrate">说明项</td>
        <td align="center"  bgcolor = "#C0C0C0" class="describe"> 描述</td>
    <tr>
    <tr>
        <td align="left">名字</td>
        <td align="left" style="font-weight: bold">removeNamedPolicies</td>
    <tr>
    <tr>
        <td align="left">作用</td>
        <td align="left">批量移除多个角色的多个权限<br>注意：只有所有权限操作成功才会成功，否则存在一个操作失败则整体失败</td>
    <tr>
    <tr>
        <td align="left">举例</td>
        <td align="left">移除<nobr  style="font-weight: bold">系统管理员1</nobr>发送 DELETE 请求到 /api/v1/mock/status 权限<br>移除<nobr  style="font-weight: bold">机构管理员2</nobr>发送 GET 请求到 api/v1/role/* 权限</td>
    <tr>
    <tr>
        <td align="left">使用</td>
        <td align="left">见下面代码块所示</td>
    <tr>
        <tr>
        <td align="left">返回说明</td>
        <td align="left">true: 操作成功<br>false:操作失败</td>
    <tr>
</table>

```js
client.removeNamedPolicies([
      ['系统管理员1', '/api/v1/mock/status', 'DELETE'],
      ['机构管理员2', 'api/v1/role/*', 'GET']
])
```

## 15. 移除某个用户拥有的某个角色
<table>
    <tr class="title">
        <td align="center"  bgcolor = "#C0C0C0" class="illustrate">说明项</td>
        <td align="center"  bgcolor = "#C0C0C0" class="describe"> 描述</td>
    <tr>
    <tr>
        <td align="left">名字</td>
        <td align="left" style="font-weight: bold">deleteRoleForUser</td>
    <tr>
    <tr>
        <td align="left">作用</td>
        <td align="left">移除某个用户拥有的某个角色<br>是 addRoleForUser 的逆向操作</td>
    <tr>
    <tr>
        <td align="left">举例</td>
        <td align="left">移除<nobr  style="font-weight: bold">hyx</nobr>这个用户的<nobr  style="font-weight: bold">系统管理员1</nobr>身份</td>
    <tr>
    <tr>
        <td align="left">使用</td>
        <td align="left">client.deleteRoleForUser("hyx", '系统管理员1')</td>
    <tr>
        <tr>
        <td align="left">返回说明</td>
        <td align="left">true: 操作成功<br>false:操作失败</td>
    <tr>
</table>
