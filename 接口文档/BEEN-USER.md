# BEEN-USER

## 接口设计
 
### 1. 用户管理

#### 1.1 查看详情

```
url: 3001/user/auth/user/read/{id}
method: GET
param: text
return: json
{
    "errno": 0,
    "data": {
        "id": 1,
        "name": "用户名称",  
        "code": "用户编号",  
        "username": "111",  // 账号
        "password": "userPwd",  // 密码, 被隐藏只会得到userPwd
        "authPwd": "authPwd",  // 访问密码, 被隐藏只会得到authPwd
        "trustAdmin": null,  // 委托内容管理员id
        "trustUser": null,  // 委托用户id
        "roleType": 1,  // 角色类型, 0-未知, 1-超管, 2-编辑, 3-审核, 4-普通
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
        "qrCode": "",  // 二维码
        "trustAdminName": "委托内容管理员姓名",
        "trustUserName": "委托内容管理员姓名"
    },
    "errmsg": "成功"
}      
error: 502, 510, 201
```

#### 1.2 列表查询  

```
url: 3001/user/auth/user/list
method: GET
param: text
{
    name: "名称", 
    code: "编号", 
    trustAdmin: 1,  // 委托管理员id
    roleType: 0, 1  // 角色集合, 2-编辑, 3-审核, 4-普通
    con: "通用条件",  // 可模糊匹配账号, 昵称
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
                "name": "用户名称",  
                "code": "用户编号",  
                "username": "111",  // 账号
                "password": "userPwd",  // 密码, 被隐藏只会得到userPwd
                "authPwd": "authPwd",  // 访问密码, 被隐藏只会得到authPwd
                "trustAdmin": null,  // 委托内容管理员id
                "trustUser": null,  // 委托用户id
                "roleType": 1,  // 角色类型, 0-未知, 1-超管, 2-编辑, 3-审核, 4-普通
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
                "qrCode": "",  // 二维码
                "trustAdminName": "委托内容管理员姓名",
                "trustUserName": "委托内容管理员姓名"
            }
        ]
    },
    "errmsg": "成功"
}      
error: 502, 504
```

#### 1.3 编辑

```
url: 3001/user/auth/user/edit
remark: 普通编辑只允许修改姓名, 昵称, 生日, 头像, 性别, 身份证;
    邮箱等基础信息roleType与trustAdmin只有超管操作时才传
method: POST
param: json
{
    "id": 1,
    "name": "用户名称",  
    "password": "userPwd",  // 密码
    "authPwd": "authPwd",  // 访问密码
    "nickname": "111",  // 昵称
    "trustAdmin": 1,  // 委托用户id
    "trustUser": 1,  // 委托用户id
    "roleType": 1,  // 角色类型, 2-编辑, 3-审核, 4-普通 只有超级管理员才能设置
    "avatar": "aaa",  // 头像地址
    "logoUrl": "aaa",  // 肖像地址
    "backUrl": "aaa",  // 背景地址
    "idCard": "",  // 身份证
    "mail": "111111",  // 邮箱
    "gender": 0,  // 性别, 0-未知, 1-男, 2-女
    "birthday": "2019-05-17",
    "remark": "111111"
}
return: json
{
    "errno": 0,
    "data": {
        "id": 1,
        "name": "用户名称",  
        "code": "用户编号",  
        "username": "111",  // 账号
        "password": "userPwd",  // 密码, 被隐藏只会得到userPwd
        "authPwd": "authPwd",  // 访问密码, 被隐藏只会得到authPwd
        "trustAdmin": 1,  // 委托内容管理员id
        "trustUser": 1,  // 委托用户id
        "roleType": 1,  // 角色类型, 0-未知, 1-超管, 2-编辑, 3-审核, 4-普通
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
        "qrCode": "",  // 二维码
        "trustAdminName": "委托内容管理员姓名",
        "trustUserName": "委托内容管理员姓名"
    },
    "errmsg": "成功"
}      
error: 502, 503, 510
```

#### 1.4 当前用户基本信息

```
url: 3001/user/auth/user/info
method: GET
param: null
return: json
{
    "errno": 0,
    "data": {
        "id": 1,
        "name": "用户名称",  
        "code": "用户编号",  
        "username": "111",  // 账号
        "password": "userPwd",  // 密码, 被隐藏只会得到userPwd
        "authPwd": "authPwd",  // 访问密码, 被隐藏只会得到authPwd
        "trustAdmin": null,  // 委托内容管理员id
        "trustUser": null,  // 委托用户id
        "roleType": 1,  // 角色类型, 0-未知, 1-超管, 2-编辑, 3-审核, 4-普通
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
        "qrCode": "",  // 二维码
        "trustAdminName": "委托内容管理员姓名",
        "trustUserName": "委托内容管理员姓名"
    },
    "errmsg": "成功"
}      
error: 502, 510, 201
```

#### 1.5 当前用户带权限信息

```
url: 3001/user/auth/user/info/perms
method: GET
param: null
return: json
{
    "errno": 0,
    "data": {
        "id": 1,
        "name": "用户名称",  
        "code": "用户编号",  
        "username": "111",  // 账号
        "password": "userPwd",  // 密码, 被隐藏只会得到userPwd
        "authPwd": "authPwd",  // 访问密码, 被隐藏只会得到authPwd
        "trustAdmin": null,  // 委托内容管理员id
        "trustUser": null,  // 委托用户id
        "roleType": 1,  // 角色类型, 0-未知, 1-超管, 2-编辑, 3-审核, 4-普通
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
        "qrCode": "",  // 二维码
        "trustAdminName": "委托内容管理员姓名",
        "trustUserName": "委托内容管理员姓名"
        // 权限集合
        "perms": [
            "/test"
        ]
    },
    "errmsg": "成功"
}      
error: 502, 510, 201
```

#### 1.6 分配账号

```
url: 3001/user/auth/user/allocate
remark: 只有超管才能分配账号, 并且以手机号作为账号, 
method: POST
param: json
{
    "name": "用户名称",  // 必填
    "code": "用户编号",  // 必填且一旦设定不允许变更 
    "mobile": "手机号",  // 必填
    "password": "userPwd",  // 密码, 必填
    "authPwd": "authPwd",  // 访问密码
    "nickname": "111",  // 昵称
    "trustAdmin": null,  // 委托内容管理员id, 只有超级管理员才能设置
    "trustUser": null,  // 委托用户id
    "roleType": 1,  // 角色类型, 2-编辑, 3-审核, 4-普通 只有超级管理员才能设置
    "avatar": "aaa",  // 头像地址
    "logoUrl": "aaa",  // 肖像地址
    "backUrl": "aaa",  // 背景地址
    "idCard": "",  // 身份证
    "mail": "111111",  // 邮箱
    "gender": 0,  // 性别, 0-未知, 1-男, 2-女
    "birthday": "2019-05-17",
    "remark": "111111"
}
return: json
{
    "errno": 0,
    "data": {
        "id": 1,
        "name": "用户名称",  
        "code": "用户编号",  
        "username": "111",  // 账号
        "password": "userPwd",  // 密码, 被隐藏只会得到userPwd
        "authPwd": "authPwd",  // 访问密码, 被隐藏只会得到authPwd
        "trustAdmin": null,  // 委托内容管理员id
        "trustUser": null,  // 委托用户id
        "roleType": 1,  // 角色类型, 0-未知, 1-超管, 2-编辑, 3-审核, 4-普通
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
        "qrCode": "",  // 二维码
        "trustAdminName": "委托内容管理员姓名",
        "trustUserName": "委托内容管理员姓名"
    },
    "errmsg": "成功"
}      
error: 502, 503, 510, 205, 206
```

#### 1.7 根据编码获取详情

```
url: 3001/user/auth/user/read/code/{code}
method: GET
param: text
return: json
{
    "errno": 0,
    "data": {
        "id": 1,
        "name": "用户名称",  
        "code": "用户编号",  
        "username": "111",  // 账号
        "password": "userPwd",  // 密码, 被隐藏只会得到userPwd
        "authPwd": "authPwd",  // 访问密码, 被隐藏只会得到authPwd
        "trustAdmin": null,  // 委托内容管理员id
        "trustUser": null,  // 委托用户id
        "roleType": 1,  // 角色类型, 0-未知, 1-超管, 2-编辑, 3-审核, 4-普通
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
        "qrCode": "",  // 二维码
        "trustAdminName": "委托内容管理员姓名",
        "trustUserName": "委托内容管理员姓名"
    },
    "errmsg": "成功"
}      
error: 502, 510, 201
```

#### 1.8 删除用户

```
url: 3001/user/auth/user/del
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
