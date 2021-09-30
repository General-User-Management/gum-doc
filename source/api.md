# 客户端API列表
## 1. 给角色增加一个api权限
说明项 | 描述
--- |--- |
名字 | **addPolicy**
作用 | 给某个角色增加一个API接口的权限
举例 | 给`系统管理员`增加`POST`请求到URL为`/api/v1/mock/status`的权限 
使用 | client.addPolicy("系统管理员", "/api/v1/mock/status", "POST")

## 2. 批量增加p域
说明项 | 描述
--- |--- |
名字 | **addPolicies**
作用 | 批量给多个不同角色赋予不同权限
举例 | 给`系统管理员1`增加`GET`、`POST`、`PUT`、`PATCH`、`DELETE`请求到URL为`api/v1/users`的权限；给`系统管理员2`增加`GET`请求到URL为`api/v1/role`为前缀的权限；给`系统管理员3`增加`POST`请求到URL为`api/v1/school/:schoolid/teacher/:teacherid`的RESTful的权限
使用 | 见下面的代码块
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
说明项 | 描述
--- |--- |
名字 | **addRoleForUser**
作用 | 给某个用户赋予某个角色（某个角色里面增加某个用户）
举例 | 给`zhangsan`这个用户赋予为`管理员`这个角色
使用 | client.addRoleForUser("zhangsan", "管理员")
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
