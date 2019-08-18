# BEEN-SYSTEM

## 接口设计

### 1. 权限(perm)管理

#### 1.1 查看详情

```
url: 3001/user/auth/perm/read/{id}
method: GET
param: text
return: json
{
    "errno": 0,
    "data": {
        "id": 1,
        "name": "测试权限",
        "permUrl": "/test",
        "menuStatus": 0,  // 是否菜单, 0-否, 1-是
        "anonStatus": 0,  // 匿名权限, 0-否, 1-是
        "remark": "111",
        "addTime": "2019-05-17T17:22:04",
        "updateTime": null,
        "deleted": false
    },
    "errmsg": "成功"
}      
error: 502, 510, 103
```

#### 1.2 列表查询  

```
url: 3001/user/auth/perm/list
method: GET
param: text
{
    name: "名称", 
    menuStatus: 0,  // 是否菜单, 0-否, 1-是
    anonStatus: 0,  // 匿名权限, 0-否, 1-是
    page: 1,    // 页数
    limit: 10,    // 每页容量
    sort: "update_time",    // 排序字段
    order: "desc",    // 排序规则
}
return: json
{
    "errno": 0,
    "data": {
        "total": 1,
        "items": [
            {
                "id": 1,
                "name": "测试权限",
                "permUrl": "/test",
                "menuStatus": 0,  // 是否菜单, 0-否, 1-是
                "anonStatus": 0,  // 匿名权限, 0-否, 1-是
                "remark": "111",
                "addTime": "2019-05-17T17:22:04",
                "updateTime": null,
                "deleted": false
            }
        ]
    },
    "errmsg": "成功"
}      
error: 502, 504
```

#### 1.3 添加

```
url: 3001/user/auth/perm/add
method: POST
param: json
{
    "name": "测试权限",
    "permUrl": "/test",
    "menuStatus": 0,
    "anonStatus": 0
}
return: json
{
    "errno": 0,
    "data": {
        "id": 1,
        "name": "测试权限",
        "permUrl": "/test",
        "menuStatus": 0,  // 是否菜单, 0-否, 1-是
        "anonStatus": 0,  // 匿名权限, 0-否, 1-是
        "remark": "111",
        "addTime": "2019-05-17T17:22:04",
        "updateTime": null,
        "deleted": false
    },
    "errmsg": "成功"
}      
error: 502, 503
```

#### 1.4 编辑

```
url: 3001/user/auth/perm/edit
method: POST
param: json
{
    "id": 1,
    "name": "测试权限",
    "permUrl": "/test",
    "menuStatus": 0,  // 是否菜单, 0-否, 1-是
    "anonStatus": 0,  // 匿名权限, 0-否, 1-是
}
return: json
{
    "errno": 0,
    "data": {
        "id": 1,
        "name": "测试权限",
        "permUrl": "/test",
        "menuStatus": 0,  // 是否菜单, 0-否, 1-是
        "anonStatus": 0,  // 匿名权限, 0-否, 1-是
        "remark": "111",
        "addTime": "2019-05-17T17:22:04",
        "updateTime": null,
        "deleted": false
    },
    "errmsg": "成功"
}      
error: 502, 503, 510
```

#### 1.5 删除

```
url: 3001/user/auth/perm/del
method: GET
param: text
{
    ids: 1,2,3  // 主键集
}
return: json
{
    "errno": 0,
    "errmsg": "成功"
}      
error: 502, 503
```

### 2. 角色管理

#### 2.1 查看详情

```
url: 3001/user/auth/role/read/{id}
method: GET
param: text
return: json
{
    "errno": 0,
    "data": {
        "id": 1,
        "name": "测试角色",
        "remark": null,
        "addTime": "2019-05-17T17:22:22",
        "updateTime": null,
        "deleted": false
    },
    "errmsg": "成功"
}      
error: 502, 510, 104
```

#### 2.2 列表查询  

```
url: 3001/user/auth/role/list
method: GET
param: text
{
    name: "名称", 
    page: 1,    // 页数
    limit: 10,    // 每页容量
    sort: "update_time",    // 排序字段
    order: "desc",    // 排序规则
}
return: json
{
    "errno": 0,
    "data": {
        "total": 1,
        "items": [
            {
                "id": 1,
                "name": "测试角色",
                "remark": null,
                "addTime": "2019-05-17T17:22:22",
                "updateTime": null,
                "deleted": false
            }
        ]
    },
    "errmsg": "成功"
}      
error: 502, 504
```

#### 2.3 添加

```
url: 3001/user/auth/role/add
method: POST
param: json
{
    "name": "测试权限"
}
return: json
{
    "errno": 0,
    "data": {
        "id": 1,
        "name": "测试角色",
        "remark": null,
        "addTime": "2019-05-17T17:22:22",
        "updateTime": null,
        "deleted": false
    },
    "errmsg": "成功"
}      
error: 502, 503
```

#### 2.4 编辑

```
url: 3001/user/auth/role/edit
method: POST
param: json
{
    "id": 1,
    "name": "测试角色"
}
return: json
{
    "errno": 0,
    "data": {
        "id": 1,
        "name": "测试角色",
        "remark": null,
        "addTime": "2019-05-17T17:22:22",
        "updateTime": null,
        "deleted": false
    },
    "errmsg": "成功"
}      
error: 502, 503, 510
```

#### 2.5 删除

```
url: 3001/user/auth/role/del
method: GET
param: text
{
    ids: 1,2,3  // 主键集
}
return: json
{
    "errno": 0,
    "errmsg": "成功"
}      
error: 502, 503
```
 
### 3. 授权管理

#### 3.1 查看角色-权限

```
url: 3001/user/auth/role_perm/read/{id}
method: GET
param: text
return: json
{
    "errno": 0,
    "data": {
        "id": 1,
        "roleId": 1,
        "permId": 1,
        "addTime": "2019-05-17T17:22:36",
        "updateTime": null,
        "roleName": "测试角色",
        "permName": "测试权限"
    },
    "errmsg": "成功"
}      
error: 502, 510, 104
```

#### 3.2 查看用户-角色

```
url: 3001/user/auth/user_role/read/{id}
method: GET
param: text
return: json
{
    "errno": 0,
    "data": {
        "id": 1,
        "userId": 1,
        "roleId": 1,
        "addTime": "2019-05-17T17:22:45",
        "updateTime": null,
        "username": "111",
        "nickname": "111",
        "mobile": "111111",
        "roleName": "测试角色"
    },
    "errmsg": "成功"
}      
error: 502, 510, 104
```

#### 3.3 角色-权限列表查询  

```
url: 3001/user/auth/role_perm/list
method: GET
param: text
{
    role: 1,  // 角色id
    perm: 1,  // 权限id 
    page: 1,    // 页数
    limit: 10,    // 每页容量
    sort: "update_time",    // 排序字段
    order: "desc",    // 排序规则
}
return: json
{
    "errno": 0,
    "data": {
        "total": 1,
        "items": [
            {
                "id": 1,
                "roleId": 1,
                "permId": 1,
                "addTime": "2019-05-17T17:22:36",
                "updateTime": null,
                "roleName": "测试角色",
                "permName": "测试权限"
            }
        ]
    },
    "errmsg": "成功"
}     
error: 502, 504
```

#### 3.4 用户-角色列表查询  

```
url: 3001/user/auth/user_role/list
method: GET
param: text
{
    user: 1,  // 用户id 
    role: 1,  // 角色id
    page: 1,    // 页数
    limit: 10,    // 每页容量
    sort: "update_time",    // 排序字段
    order: "desc",    // 排序规则
}
return: json
{
    "errno": 0,
    "data": {
        "total": 1,
        "items": [
            {
                "id": 1,
                "userId": 1,
                "roleId": 1,
                "addTime": "2019-05-17T17:22:45",
                "updateTime": null,
                "username": "111",
                "nickname": "111",
                "mobile": "111111",
                "roleName": "测试角色"
            }
        ]
    },
    "errmsg": "成功"
}    
error: 502, 504
```

#### 3.5 添加角色-权限

```
url: 3001/user/auth/role_perm/add
remark: 给角色赋予权限
method: POST
param: json
{
    "roleId": 0,  // 角色id
    "permId": 0  // 权限id
}
return: json
{
    "errno": 0,
    "data": {
        "id": 1,
        "roleId": 1,
        "permId": 1,
        "addTime": "2019-05-17T17:22:36",
        "updateTime": null,
        "roleName": "测试角色",
        "permName": "测试权限"
    },
    "errmsg": "成功"
}      
error: 502, 503, 105
```

#### 3.6 添加用户-角色

```
url: 3001/user/auth/user_role/add
remark: 给用户赋予角色
method: POST
param: json
{
    "userId": 0,  // 角色id
    "roleId": 0  // 权限id
}
return: json
{
    "errno": 0,
    "data": {
        "id": 1,
        "userId": 1,
        "roleId": 1,
        "addTime": "2019-05-17T17:22:45",
        "updateTime": null,
        "username": "111",
        "nickname": "111",
        "mobile": "111111",
        "roleName": "测试角色"
    },
    "errmsg": "成功"
}      
error: 502, 503, 106
```

#### 3.7 编辑角色-权限

```
url: 3001/user/auth/role_perm/edit
method: POST
param: json
{
    "id": 0,  // 主键
    "roleId": 0,  // 角色id
    "permId": 0  // 权限id
}
return: json
{
    "errno": 0,
    "data": {
        "id": 1,
        "roleId": 1,
        "permId": 1,
        "addTime": "2019-05-17T17:22:36",
        "updateTime": null,
        "roleName": "测试角色",
        "permName": "测试权限"
    },
    "errmsg": "成功"
}      
error: 502, 503, 510, 105
```

#### 3.8 编辑用户-角色

```
url: 3001/user/auth/user_role/edit
method: POST
param: json
{
    "id": 0,  // 主键
    "userId": 0,  // 角色id
    "roleId": 0  // 权限id
}
return: json
{
    "errno": 0,
    "data": {
        "id": 1,
        "userId": 1,
        "roleId": 1,
        "addTime": "2019-05-17T17:22:45",
        "updateTime": null,
        "username": "111",
        "nickname": "111",
        "mobile": "111111",
        "roleName": "测试角色"
    },
    "errmsg": "成功"
}      
error: 502, 503, 510, 106
```

#### 3.9 删除角色-权限

```
url: 3001/user/auth/role_perm/del
method: GET
param: text
{
    ids: 1,2,3  // 主键集
}
return: json
{
    "errno": 0,
    "errmsg": "成功"
}      
error: 502, 503
```

#### 3.10 删除用户-角色

```
url: 3001/user/auth/user_role/del
method: GET
param: 
{
    ids: 1,2,3  // 主键集
}
return: text
{
    "errno": 0,
    "errmsg": "成功"
}      
error: 502, 503
```

### 4. 登陆相关

#### 4.1 账号密码登陆

```
url: 3001/user/auth/login
method: POST
param: json
{
    username: "账号或手机", 
    password: "密码"
}
return: json
{
    "errno": 0,
    "data": "session_id",
    "errmsg": "成功"
}      
error: 502, 510, 202, 203, 204
```

#### 4.2 手机验证码登陆

```
url: 3001/user/auth/login/phone
method: POST
param: json
{
    mobile: "手机号", 
    captcha: "验证码"
}
return: json
{
    "errno": 0,
    "data": "session_id",
    "errmsg": "成功"
}      
error: 502, 510, 202, 203, 204
```

#### 4.3 退出登录

```
url: 3001/user/auth/logout
method: GET
param: null
return: json
{
    "errno": 0,
    "errmsg": "成功"
}      
error: 502, 501
```


#### 4.4 分配账号

```
url: 3001/user/auth/user/allocate
method: POST
param: json
{
        "mobile": "手机号",  
        "name": "用户名称",  
        "password": "密码", 
        "gender": 0,  // 性别, 0-未知, 1-男, 2-女
        "idCard": "身份证", 
        "birthday": "2019-05-17",
        "nickname": "昵称",  // 可选
        "avatar": "头像地址",  // 可选
        "logoUrl": "肖像地址",  // 可选
        "backUrl": "背景地址",  // 可选
        "mail": "邮箱",  // 可选
}
return: json
{
    "errno": 0,
    "data": {
        "id": 1,
        "name": "用户名称",  
        "username": "111",  // 账号
        "password": "userPwd",  // 密码, 被隐藏只会得到userPwd
        "authPwd": "authPwd",  // 访问密码, 被隐藏只会得到authPwd
        "trustAccount": null,  // 委托用户
        "nickname": "111",  // 昵称
        "qrCode": "",  // 二维码
        "avatar": "aaa",  // 头像地址
        "logoUrl": "aaa",  // 肖像地址
        "backUrl": "aaa",  // 背景地址
        "mobile": "111111",  // 手机号
        "idCard": "",  // 身份证
        "mail": "111111",  // 邮箱
        "gender": 0,  // 性别, 0-未知, 1-男, 2-女
        "birthday": "2019-05-17",
        "remark": "111111",
        "qrCode": ""  // 二维码
    },
    "errmsg": "成功"
}      
error: 502, 503, 205
```

