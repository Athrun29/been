# BEEN-MODULE

## 接口设计
 
### 1. 模块管理

#### 1.1 查看详情

```
url: 3002/biz/module/read/{id}
remark: 不同类型模块的子项items不一样，主要用于从模块列表进入模块编辑。
子项信息不包含富文本详情（如果有），即items.detailInfo被设置为null
method: GET
param: 模块id
return: json
{
    "errno": 0,
    "data": {
        "id": 1,
        "userId": 1,  // 数据持有人
        "name": "影集1",  // 模块名称
        "type": 0,  // 模块类型, 0-影集, 1-时间轴, 2-生平事件
        "authStatus": 2,  // 访问状态, 0-私密, 1-密码访问, 2-公开
        "auditStatus": 2,  // 审核状态, 0-待审, 1-通过, 2-拒绝
        "remark": null,
        "sort": 1,  // 顺序号
        "visible": null,  // 标识是否可忽略访问权限状态, 1-可以直接可见
        "userName": "用户名称",  
        // --- 影集子项
        "items": [
            {
                "id": 1,
                "userId": 1,  // 数据持有人
                "moduleId": 1,  // 所属模块id
                "name": "图片1",  // 名称
                "mediaUrl": "111111",  // 影像url
                "type": 0,  // 媒体类型, 0-图片, 1-视频, 2-音频
                "markTime": "2019-05-21T17:12:31",  // 时间
                "markAddr": "茶山刘女子职业技术学院",  // 地点
                "markPerson": "码农",  // 人物
                "briefInfo": "码农交流",  // 简介
                "sort": 1,
                "remark": null
            }
        ]
        // --- 时间轴子项
        "items": [
            {
                "id": 1,
                "userId": 1,  // 数据持有人
                "moduleId": 2,  // 所属模块id
                "name": "时间1",  // 名称
                "markTime": "2019-05-21T17:13:35",  // 标记时间
                "mediaUrl": "111111",  // 媒体url
                "briefInfo": "码农集会",  // 简介
                "sort": 1,  // 顺序号
                "remark": null,
                "detailInfo": null  // 富文本详情
            }
        ]
        // --- 生平事件子项
        "items": [
            {
                "id": 1,
                "userId": 1,  // 数据持有人
                "moduleId": 3,  // 所属模块id
                "name": "事件1",  // 名称
                "mediaUrl": "111111",  // 媒体url  
                "briefInfo": "码农集会",  // 简介
                "detailInfo": null,  // 富文本详情
                "sort": 1,  // 顺序号
                "remark": null
            }
        ]
    },
    "errmsg": "成功"
}     
error: 502, 507, 510
```

#### 1.2 模块预览

```
url: 3002/biz/module/preview/{id}
remark: 不同类型模块的子项items不一样，主要用于编辑完一个模块之后预览实际效果。
子项包含富文本详情
method: GET
param: 模块id
return: json
{
    "errno": 0,
    "data": {
        "id": 1,
        "userId": 1,  // 数据持有人
        "name": "影集1",  // 模块名称
        "type": 0,  // 模块类型, 0-影集, 1-时间轴, 2-生平事件
        "authStatus": 2,  // 访问状态, 0-私密, 1-密码访问, 2-公开
        "auditStatus": 2,  // 审核状态, 0-待审, 1-通过, 2-拒绝
        "remark": null,
        "sort": 1,  // 顺序号
        "visible": null,  // 标识是否可忽略访问权限状态, 1-可以直接可见
        "userName": "用户名称",  
        // --- 影集子项
        "items": [
            {
                "id": 1,
                "userId": 1,  // 数据持有人
                "moduleId": 1,  // 所属模块id
                "name": "图片1",  // 名称
                "mediaUrl": "111111",  // 影像url
                "type": 0,  // 媒体类型, 0-图片, 1-视频, 2-音频
                "markTime": "2019-05-21T17:12:31",  // 时间
                "markAddr": "茶山刘女子职业技术学院",  // 地点
                "markPerson": "码农",  // 人物
                "briefInfo": "码农交流",  // 简介
                "sort": 1,
                "remark": null
            }
        ]
        // --- 时间轴子项
        "items": [
            {
                "id": 1,
                "userId": 1,  // 数据持有人
                "moduleId": 2,  // 所属模块id
                "name": "时间1",  // 名称
                "markTime": "2019-05-21T17:13:35",  // 标记时间
                "mediaUrl": "111111",  // 媒体url
                "briefInfo": "码农集会",  // 简介
                "sort": 1,  // 顺序号
                "remark": null,
                "detailInfo": "富文本详情"
            }
        ]
        // --- 生平事件子项
        "items": [
            {
                "id": 1,
                "userId": 1,  // 数据持有人
                "moduleId": 3,  // 所属模块id
                "name": "事件1",  // 名称
                "mediaUrl": "111111",  // 媒体url  
                "briefInfo": "码农集会",  // 简介
                "detailInfo": "富文本详情"
                "sort": 1,  // 顺序号
                "remark": null
            }
        ]
    },
    "errmsg": "成功"
}     
error: 502, 507, 510
```

#### 1.3 我的模块  

```
url: 3002/biz/module/list/my
remark: 只显示当前用户的数据，用于管理当前自己的数据。
列表查询精简掉了不必要展示数据增加传输效率，如items是空数组
method: GET
param: text
{
    name: "名称", 
    type: 0,  // 模块类型, 0-影集, 1-时间轴, 2-生平事件
    authStatus: 2,  // 访问状态, 0-私密, 1-密码访问, 2-公开
    auditStatus: 2,  // 审核状态, 0-待审, 1-通过, 2-拒绝
    page: 1,    // 页数
    limit: 10,    // 每页容量
    sort: "sort",    // 排序字段
    order: "asc",    // 排序规则
}
return: json
{
    "errno": 0,
    "data": {
        "total": 3,
        "items": [
            {
                "id": 1,
                "userId": 1,
                "name": "影集1",
                "type": 0,
                "authStatus": 2,
                "auditStatus": 2,
                "remark": null,
                "sort": 1,
                "visible": null,
                "userName": "用户名称",  
                "items": []
            }
        ]
    },
    "errmsg": "成功"
}     
error: 502, 504
```

#### 1.4 委托管理列表  

```
url: 3002/biz/module/list/admin
remark: 只显示被委托管理的模块，用于管理员帮助用户编辑模块。
列表查询规则同1.3
method: GET
param: text
{
    name: "名称", 
    user: 1,  // 委托人id
    type: 0,  // 模块类型, 0-影集, 1-时间轴, 2-生平事件
    authStatus: 2,  // 访问状态, 0-私密, 1-密码访问, 2-公开
    auditStatus: 2,  // 审核状态, 0-待审, 1-通过, 2-拒绝
    page: 1,    // 页数
    limit: 10,    // 每页容量
    sort: "sort",    // 排序字段
    order: "asc",    // 排序规则
}
return: json
{
    "errno": 0,
    "data": {
        "total": 3,
        "items": [
            {
                "id": 1,
                "userId": 1,
                "name": "影集1",
                "type": 0,
                "authStatus": 2,
                "auditStatus": 2,
                "remark": null,
                "sort": 1,
                "visible": null,
                "userName": "用户名称",  
                "items": []
            }
        ]
    },
    "errmsg": "成功"
}     
error: 502, 504
```

#### 1.5 添加

```
url: 3002/biz/module/add
remark: 本人编辑自己模块数据默认将userId填写为当前用户id；
委托编辑情况下需要选择委托人id
method: POST
param: json
{
    "userId": 1,
    "name": "模块名",
    "type": 0,  // 模块类型, 0-影集, 1-时间轴, 2-生平事件
    "authStatus": 2,  // 访问状态, 0-私密, 1-密码访问, 2-公开
    "sort": 1,  // 顺序号
}
return: json
{
    "errno": 0,
    "data": {
        "id": 1,
        "userId": 1,
        "name": "模块名",
        "type": 0,
        "authStatus": 2,
        "auditStatus": 2,
        "remark": null,
        "sort": 1,
        "visible": null,
        "userName": "用户名称",  
        "items": []
    },
    "errmsg": "成功"
}      
error: 502, 503, 301, 302
```

#### 1.6 编辑

```
url: 3002/biz/module/edit
remark: 本人编辑自己模块数据默认将userId填写为当前用户id；
委托编辑情况下需要选择委托人id
method: POST
param: json
{
    "id": 1,
    "userId": 1,
    "name": "模块名",
    "type": 0,  // 模块类型, 0-影集, 1-时间轴, 2-生平事件
    "authStatus": 2,  // 访问状态, 0-私密, 1-密码访问, 2-公开
    "sort": 1,  // 顺序号
}
return: json
{
    "errno": 0,
    "data": {
        "id": 1,
        "userId": 1,
        "name": "模块名",
        "type": 0,
        "authStatus": 2,
        "auditStatus": 2,
        "remark": null,
        "sort": 1,
        "visible": null,
        "userName": "用户名称",  
        "items": []
    },
    "errmsg": "成功"
}      
error: 502, 503, 301, 302
```

#### 1.7 删除

```
url: 3002/biz/module/del
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

#### 1.8 展示  

```
url: 3002/biz/module/show/{userId}
remark: 展示某个用户的数据。
若当前用户为数据持有人会展示全部完整数据, 并且visible=1。
他人浏览则不会给visible字段赋值，不显示私密状态（authStatus=0）的模块，
需要密码访问（authStatus=1）的模块不显示子项，
只有公开状态（authStatus=2）的模块完整显示
method: GET
param: 用户id
return: json
{
    "errno": 0,
    "data": [
        {
            "id": 1,
            "userId": 1,
            "name": "影集1",
            "type": 0,
            "authStatus": 2,
            "auditStatus": 2,
            "remark": null,
            "sort": 1,
            "visible": null,
            "userName": "用户名称",  
            "items": [
                {
                    "id": 1,
                    "userId": 1,
                    "moduleId": 1,
                    "name": "图片1",
                    "mediaUrl": "111111",
                    "type": 0,  // 媒体类型, 0-图片, 1-视频, 2-音频
                    "markTime": "2019-05-21T17:12:31",
                    "markAddr": "茶山刘女子职业技术学院",
                    "markPerson": "码农",
                    "briefInfo": "码农交流",
                    "sort": 1,
                    "remark": null
                }
            ]
        },
        {
            "id": 2,
            "userId": 1,
            "name": "时间轴1",
            "type": 1,
            "authStatus": 1,
            "remark": null,
            "sort": 2,
            "visible": null,
            "items": []
        }
    ],
    "errmsg": "成功"
}    
error: 502, 504
```

#### 1.9 密码访问

```
url: 3002/biz/module/visit
remark: 密码配对成功会返回该模块完整数据
method: POST
param: json
{
    "module": 1,  // 模块id
    "authPwd": "访问密码"
}
return: json
{
    "errno": 0,
    "data": {
        "id": 2,
        "userId": 1,
        "name": "时间轴1",
        "type": 1,
        "authStatus": 1,
        "auditStatus": 2,
        "remark": null,
        "sort": 2,
        "visible": null,
        "userName": "用户名称",  
        // --- 影集子项
        "items": [
            {
                "id": 1,
                "userId": 1,  // 数据持有人
                "moduleId": 1,  // 所属模块id
                "name": "图片1",  // 名称
                "mediaUrl": "111111",  // 影像url
                "type": 0,  // 媒体类型, 0-图片, 1-视频, 2-音频
                "markTime": "2019-05-21T17:12:31",  // 时间
                "markAddr": "茶山刘女子职业技术学院",  // 地点
                "markPerson": "码农",  // 人物
                "briefInfo": "码农交流",  // 简介
                "sort": 1,
                "remark": null
            }
        ]
        // --- 时间轴子项
        "items": [
            {
                "id": 1,
                "userId": 1,  // 数据持有人
                "moduleId": 2,  // 所属模块id
                "name": "时间1",  // 名称
                "markTime": "2019-05-21T17:13:35",  // 标记时间
                "mediaUrl": "111111",  // 媒体url
                "briefInfo": "码农集会",  // 简介
                "sort": 1,  // 顺序号
                "remark": null,
                "detailInfo": "富文本详情"
            }
        ]
        // --- 生平事件子项
        "items": [
            {
                "id": 1,
                "userId": 1,  // 数据持有人
                "moduleId": 3,  // 所属模块id
                "name": "事件1",  // 名称
                "mediaUrl": "111111",  // 媒体url  
                "briefInfo": "码农集会",  // 简介
                "detailInfo": "富文本详情"
                "sort": 1,  // 顺序号
                "remark": null
            }
        ]
    },
    "errmsg": "成功"
}     
error: 502, 503, 303, 304
```
 
#### 1.10 变更访问状态

```
url: 3002/biz/module/edit/auth
method: GET
param: text
{
    id: 1,  // 模块id
    authStatus: 2,  // 访问状态, 0-私密, 1-密码访问, 2-公开
}
return: json
{
    "errno": 0,
    "errmsg": "成功"
}      
error: 502, 503, 507, 302
```

#### 1.11 模块审核

```
url: 3002/biz/module/audit
method: GET
param: text
{
    id: 1,  // 模块id
    auditStatus: 2,  // 审核状态, 0-待审, 1-通过, 2-拒绝
}
return: json
{
    "errno": 0,
    "errmsg": "成功"
}      
error: 502, 503, 507, 302
```

#### 1.12 所有模块(list)  

```
url: 3002/biz/module/list
remark: 所有模块
列表查询规则同1.3
method: GET
param: text
{
    name: "名称", 
    user: 1,  // 委托人id
    type: 0,  // 模块类型, 0-影集, 1-时间轴, 2-生平事件
    authStatus: 2,  // 访问状态, 0-私密, 1-密码访问, 2-公开
    auditStatus: 2,  // 审核状态, 0-待审, 1-通过, 2-拒绝
    page: 1,    // 页数
    limit: 10,    // 每页容量
    sort: "sort",    // 排序字段
    order: "asc",    // 排序规则
}
return: json
{
    "errno": 0,
    "data": {
        "total": 3,
        "items": [
            {
                "id": 1,
                "userId": 1,
                "name": "影集1",
                "type": 0,
                "authStatus": 2,
                "auditStatus": 2,
                "remark": null,
                "sort": 1,
                "visible": null,
                "userName": "用户名称",  
                "items": []
            }
        ]
    },
    "errmsg": "成功"
}     
error: 502, 504
```

### 2 影集管理

#### 2.1 查看详情

```
url: 3002/biz/module/album/read/{id}
method: GET
param: 影像id
return: json
{
    "errno": 0,
    "data": {
        "id": 1,
        "userId": 1,  // 用户id
        "moduleId": 1,  // 模块id
        "name": "影像名", 
        "mediaUrl": "影像url",
        "type": 0,  // 媒体类型, 0-图片, 1-视频, 2-音频
        "markTime": "2019-05-21T17:12:31",  // 时间
        "markAddr": "茶山刘女子职业技术学院",  // 地点
        "markPerson": "码农",  // 人物
        "briefInfo": "码农交流",  // 简介
        "sort": 1,  // 顺序号
        "remark": null
    },
    "errmsg": "成功"
}     
error: 502, 510
```

#### 2.2 添加

```
url: 3002/biz/album/add
method: POST
param: json
{
    "userId": 1,  // 直接取上级页面中模块的userId
    "moduleId": 1,  // 直接取上级页面中模块id
    "name": "影像名", 
    "mediaUrl": "影像url",
    "type": 0,  // 媒体类型, 0-图片, 1-视频, 2-音频
    "markTime": "2019-05-21T17:12:31",  // 时间
    "markAddr": "茶山刘女子职业技术学院",  // 地点
    "markPerson": "码农",  // 人物
    "briefInfo": "码农交流",  // 简介
    "sort": 1,  // 顺序号
    "remark": "备注"  // 可选
}
return: json
{
    "errno": 0,
    "data": {
        "id": 1,
        "userId": 1,  // 用户id
        "moduleId": 1,  // 模块id
        "name": "影像名", 
        "mediaUrl": "影像url",
        "type": 0,  // 媒体类型, 0-图片, 1-视频, 2-音频
        "markTime": "2019-05-21T17:12:31",  // 时间
        "markAddr": "茶山刘女子职业技术学院",  // 地点
        "markPerson": "码农",  // 人物
        "briefInfo": "码农交流",  // 简介
        "sort": 1,  // 顺序号
        "remark": null
    },
    "errmsg": "成功"
}      
error: 502, 503
```

#### 2.3 编辑

```
url: 3002/biz/album/edit
method: POST
param: json
{
    "id": 1,
    "userId": 1,  // 直接取上级页面中模块的userId
    "moduleId": 1,  // 直接取上级页面中模块id
    "name": "影像名", 
    "mediaUrl": "影像url",
    "type": 0,  // 媒体类型, 0-图片, 1-视频, 2-音频
    "markTime": "2019-05-21T17:12:31",  // 时间
    "markAddr": "茶山刘女子职业技术学院",  // 地点
    "markPerson": "码农",  // 人物
    "briefInfo": "码农交流",  // 简介
    "sort": 1,  // 顺序号
    "remark": "备注"  // 可选
}
return: json
{
    "errno": 0,
    "data": {
        "id": 1,
        "userId": 1,  // 用户id
        "moduleId": 1,  // 模块id
        "name": "影像名", 
        "mediaUrl": "影像url",
        "type": 0,  // 媒体类型, 0-图片, 1-视频, 2-音频
        "markTime": "2019-05-21T17:12:31",  // 时间
        "markAddr": "茶山刘女子职业技术学院",  // 地点
        "markPerson": "码农",  // 人物
        "briefInfo": "码农交流",  // 简介
        "sort": 1,  // 顺序号
        "remark": null
    },
    "errmsg": "成功"
}      
error: 502, 503
```

#### 2.4 删除

```
url: 3002/biz/album/del
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

#### 2.5 批量添加

```
url: 3002/biz/album/add/batch
method: POST
param: json
{
    "userId": 1,  // 直接取上级页面中模块的userId
    "moduleId": 1,  // 直接取上级页面中模块id
    "name": "影像名", 
    "type": 0,  // 媒体类型, 0-图片, 1-视频, 2-音频
    "markTime": "2019-05-21T17:12:31",  // 时间
    "markAddr": "茶山刘女子职业技术学院",  // 地点
    "markPerson": "码农",  // 人物
    "briefInfo": "码农交流",  // 简介
    "sort": 1,  // 顺序号
    "remark": "备注"  // 可选
    "urls": ["url1", "url2"]  // 文件url列表
}
return: json
{
    "errno": 0,
    "data": [
        {
            "id": 1,
            "userId": 1,  // 用户id
            "moduleId": 1,  // 模块id
            "name": "影像名", 
            "mediaUrl": "影像url",
            "type": 0,  // 媒体类型, 0-图片, 1-视频, 2-音频
            "markTime": "2019-05-21T17:12:31",  // 时间
            "markAddr": "茶山刘女子职业技术学院",  // 地点
            "markPerson": "码农",  // 人物
            "briefInfo": "码农交流",  // 简介
            "sort": 1,  // 顺序号
            "remark": null
        }],
    "errmsg": "成功"
}      
error: 502, 503
```

### 3 时间轴管理

#### 3.1 查看详情

```
url: 3002/biz/timeline/read/{id}
method: GET
param: 影像id
return: json
{
    "errno": 0,
    "data": {
        "id": 1,
        "userId": 1,  // 用户id
        "moduleId": 2,  // 模块id
        "name": "名称",
        "markTime": "2019-05-21T17:13:35",  // 标记时间
        "mediaUrl": "111111",  // 影像url
        "briefInfo": "码农集会",  // 简介
        "sort": 1,  // 顺序号
        "remark": "备注", 
        "detailInfo": "富文本详情"
    },
    "errmsg": "成功"
}     
error: 502, 510
```

#### 3.2 添加

```
url: 3002/biz/timeline/add
method: POST
param: json
{
    "userId": 1,  // 直接取上级页面中模块的userId
    "moduleId": 1,  // 直接取上级页面中模块id
    "name": "名称",
    "markTime": "2019-05-21T17:13:35",  // 标记时间
    "mediaUrl": "111111",  // 影像url
    "briefInfo": "码农集会",  // 简介
    "sort": 1,  // 顺序号
    "remark": "备注"  // 可选
    "detailInfo": "富文本详情"
}
return: json
{
    "errno": 0,
    "data": {
        "id": 1,
        "userId": 1,  // 用户id
        "moduleId": 2,  // 模块id
        "name": "名称",
        "markTime": "2019-05-21T17:13:35",  // 标记时间
        "mediaUrl": "111111",  // 影像url
        "briefInfo": "码农集会",  // 简介
        "sort": 1,  // 顺序号
        "remark": "备注", 
        "detailInfo": "富文本详情"
    },
    "errmsg": "成功"
}      
error: 502, 503
```

#### 3.3 编辑

```
url: 3002/biz/timeline/edit
method: POST
param: json
{
    "id": 1,
    "userId": 1,  // 直接取上级页面中模块的userId
    "moduleId": 1,  // 直接取上级页面中模块id
    "name": "名称",
    "markTime": "2019-05-21T17:13:35",  // 标记时间
    "mediaUrl": "111111",  // 影像url
    "briefInfo": "码农集会",  // 简介
    "sort": 1,  // 顺序号
    "remark": "备注"  // 可选
    "detailInfo": "富文本详情"
}
return: json
{
    "errno": 0,
    "data": {
        "id": 1,
        "userId": 1,  // 用户id
        "moduleId": 2,  // 模块id
        "name": "名称",
        "markTime": "2019-05-21T17:13:35",  // 标记时间
        "mediaUrl": "111111",  // 影像url
        "briefInfo": "码农集会",  // 简介
        "sort": 1,  // 顺序号
        "remark": "备注", 
        "detailInfo": "富文本详情"
    },
    "errmsg": "成功"
}      
error: 502, 503
```

#### 3.4 删除

```
url: 3002/biz/timeline/del
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

### 4 生平事件管理

#### 4.1 查看详情

```
url: 3002/biz/event/read/{id}
method: GET
param: 影像id
return: json
{
    "errno": 0,
    "data": {
        "id": 1,
        "userId": 1,  // 用户id
        "moduleId": 3,  // 模块id
        "name": "名称",
        "mediaUrl": "111111",  // 影像url
        "briefInfo": "码农集会",  // 简介
        "sort": 1,  // 顺序号
        "remark": "备注", 
        "detailInfo": "富文本详情"
    },
    "errmsg": "成功"
}     
error: 502, 510
```

#### 4.2 添加

```
url: 3002/biz/event/add
method: POST
param: json
{
    "userId": 1,  // 直接取上级页面中模块的userId
    "moduleId": 1,  // 直接取上级页面中模块id
    "name": "名称",
    "mediaUrl": "111111",  // 影像url
    "briefInfo": "码农集会",  // 简介
    "sort": 1,  // 顺序号
    "remark": "备注"  // 可选
    "detailInfo": "富文本详情"
}
return: json
{
    "errno": 0,
    "data": {
        "id": 1,
        "userId": 1,  // 用户id
        "moduleId": 3,  // 模块id
        "name": "名称",
        "mediaUrl": "111111",  // 影像url
        "briefInfo": "码农集会",  // 简介
        "sort": 1,  // 顺序号
        "remark": "备注", 
        "detailInfo": "富文本详情"
    },
    "errmsg": "成功"
}      
error: 502, 503
```

#### 4.3 编辑

```
url: 3002/biz/event/edit
method: POST
param: json
{
    "id": 1,
    "userId": 1,  // 直接取上级页面中模块的userId
    "moduleId": 1,  // 直接取上级页面中模块id
    "name": "名称",
    "mediaUrl": "111111",  // 影像url
    "briefInfo": "码农集会",  // 简介
    "sort": 1,  // 顺序号
    "remark": "备注"  // 可选
    "detailInfo": "富文本详情"
}
return: json
{
    "errno": 0,
    "data": {
        "id": 1,
        "userId": 1,  // 用户id
        "moduleId": 3,  // 模块id
        "name": "名称",
        "mediaUrl": "111111",  // 影像url
        "briefInfo": "码农集会",  // 简介
        "sort": 1,  // 顺序号
        "remark": "备注", 
        "detailInfo": "富文本详情"
    },
    "errmsg": "成功"
}      
error: 502, 503
```

#### 4.4 删除

```
url: 3002/biz/event/del
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

### 5 生平简介管理

#### 5.1 查看详情

```
url: 3002/biz/intro/read/{id}
method: GET
param: text
return: json
{
    "errno": 0,
    "data": {
        "id": 1,
        "userId": 1,  // 所属用户id
        "name": "aaa",  // 标题
        "motto": "bbb",  // 座右铭
        "briefInfo": "111",  // 简介
        "detailInfo": null,  // 富文本详情
        "auditStatus": 0,  // 审核状态, 0-待审, 1-通过, 2-拒绝
        "remark": null,
        "addTime": "2019-06-05T16:35:50",
        "updateTime": null,
        "userName": "管理员"  // 所属用户姓名
    },
    "errmsg": "成功"
}      
error: 502, 510, 507
```

#### 5.2 根据用户id查看详情

```
url: 3002/biz/intro/read/user/{id}
method: GET
param: text, 用户的id
return: json
{
    "errno": 0,
    "data": {
        "id": 1, 
        "userId": 1,  // 所属用户id
        "name": "aaa",  // 标题
        "motto": "bbb",  // 座右铭
        "briefInfo": "111",  // 简介
        "detailInfo": null,  // 富文本详情
        "auditStatus": 0,  // 审核状态, 0-待审, 1-通过, 2-拒绝
        "remark": null,
        "addTime": "2019-06-05T16:35:50",
        "updateTime": null,
        "userName": "管理员"  // 所属用户姓名
    },
    "errmsg": "成功"
}      
error: 502, 510, 507
```

#### 5.3 列表查询  

```
url: 3002/biz/intro/list
method: GET
param: text
{
    name: "名称", 
    user: 1,  // 用户id
    auditStatus: 2,  // 审核状态, 0-待审, 1-通过, 2-拒绝
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
                "name": "专家1",
                "gender": 1,  // 性别, 0-未知, 1-男, 2-女
                "field": "搬砖",
                "briefIntroduction": "工地之星",  // 简介
                "description": "<p>工地荣誉</p>",  // 详情
                "collectNum": 100,  // 收藏数
                "pictureUrl": "url",
                "backUrl": "url",
                "addTime": "2019-05-19 12:02:58",
                "updateTime": "2019-05-19 12:04:22",
                "deleted": false
            }
        ]
    },
    "errmsg": "成功"
}      
error: 502, 504
```

#### 5.4 内容管理员对应列表查询  

```
url: 3002/biz/intro/list/admin
method: GET
param: text
{
    name: "名称", 
    user: 1,  // 用户id
    auditStatus: 2,  // 审核状态, 0-待审, 1-通过, 2-拒绝
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
                "userId": 1,  // 所属用户id
                "name": "aaa",  // 标题
                "motto": "bbb",  // 座右铭
                "briefInfo": "111",  // 简介
                "detailInfo": null,  // 富文本详情
                "auditStatus": 0,  // 审核状态, 0-待审, 1-通过, 2-拒绝
                "remark": null,
                "addTime": "2019-06-05T16:35:50",
                "updateTime": null,
                "userName": "管理员"  // 所属用户姓名
            }
        ]
    },
    "errmsg": "成功"
}      
error: 502, 504
```

#### 5.5 添加

```
url: 3002/biz/intro/add
method: POST
param: json
{
    "userId": 1,  // 所属用户id
    "name": "aaa",  // 标题
    "motto": "bbb",  // 座右铭
    "briefInfo": "111",  // 简介
    "detailInfo": null,  // 富文本详情
    "auditStatus": 0,  // 审核状态, 0-待审, 1-通过, 2-拒绝
    "remark": null
}
return: json
{
    "errno": 0,
    "data": {
        "id": 1, 
        "userId": 1,  // 所属用户id
        "name": "aaa",  // 标题
        "motto": "bbb",  // 座右铭
        "briefInfo": "111",  // 简介
        "detailInfo": null,  // 富文本详情
        "auditStatus": 0,  // 审核状态, 0-待审, 1-通过, 2-拒绝
        "remark": null,
        "addTime": "2019-06-05T16:35:50",
        "updateTime": null,
        "userName": "管理员"  // 所属用户姓名
    },
    "errmsg": "成功"
}      
error: 502, 503, 402
```

#### 5.6 编辑

```
url: 3002/biz/intro/edit
method: POST
param: json
{
    "id": 1,  // 主键 
    "userId": 1,  // 所属用户id
    "name": "aaa",  // 标题
    "motto": "bbb",  // 座右铭
    "briefInfo": "111",  // 简介
    "detailInfo": null,  // 富文本详情
    "auditStatus": 0,  // 审核状态, 0-待审, 1-通过, 2-拒绝
    "remark": null
}
return: json
{
    "errno": 0,
    "data": {
        "id": 1, 
        "userId": 1,  // 所属用户id
        "name": "aaa",  // 标题
        "motto": "bbb",  // 座右铭
        "briefInfo": "111",  // 简介
        "detailInfo": null,  // 富文本详情
        "auditStatus": 0,  // 审核状态, 0-待审, 1-通过, 2-拒绝
        "remark": null,
        "addTime": "2019-06-05T16:35:50",
        "updateTime": null,
        "userName": "管理员"  // 所属用户姓名
    },
    "errmsg": "成功"
}      
error: 502, 503
```

#### 5.7 删除

```
url: 3002/biz/intro/del
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

#### 5.8 简介审核

```
url: 3002/biz/intro/audit
method: GET
param: text
{
    id: 1,  // 简介id
    auditStatus: 2,  // 审核状态, 0-待审, 1-通过, 2-拒绝
}
return: json
{
    "errno": 0,
    "errmsg": "成功"
}      
error: 502, 503, 507, 403
```

### 6 自定义特别信息管理

#### 6.1 查看详情

```
url: 3002/biz/special/read/{id}
method: GET
param: text
return: json
{
    "errno": 0,
    "data": {
        "id": 1,
        "userId": 1,  // 所属用户id
        "name": "aaa",  // 标题
        "briefInfo": "111",  // 简介
        "detailInfo": null,  // 富文本详情
        "auditStatus": 0,  // 审核状态, 0-待审, 1-通过, 2-拒绝
        "visitStatus": 0,  // 访问状态, 0-私密, 1-公开
        "remark": null,
        "addTime": "2019-06-05T16:35:50",
        "updateTime": null,
        "userName": "管理员"  // 所属用户姓名
    },
    "errmsg": "成功"
}      
error: 502, 510, 507
```

#### 6.2 根据用户id查看详情

```
url: 3002/biz/special/read/user/{id}
method: GET
param: text, 用户的id
return: json
{
    "errno": 0,
    "data": [
        {
            "id": 1,
            "userId": 1,  // 所属用户id
            "name": "aaa",  // 标题
            "briefInfo": "111",  // 简介
            "detailInfo": null,  // 富文本详情
            "auditStatus": 0,  // 审核状态, 0-待审, 1-通过, 2-拒绝
            "visitStatus": 0,  // 访问状态, 0-私密, 1-公开
            "remark": null,
            "addTime": "2019-06-05T16:35:50",
            "updateTime": null,
            "userName": "管理员"  // 所属用户姓名
        }],
    "errmsg": "成功"
}      
error: 502, 510, 507
```

#### 6.3 列表查询  

```
url: 3002/biz/special/list
method: GET
param: text
{
    name: "名称", 
    user: 1,  // 用户id
    auditStatus: 2,  // 审核状态, 0-待审, 1-通过, 2-拒绝
    visitStatus: 0,  // 访问状态, 0-私密, 1-公开
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
                "userId": 1,  // 所属用户id
                "name": "aaa",  // 标题
                "briefInfo": "111",  // 简介
                "detailInfo": null,  // 富文本详情
                "auditStatus": 0,  // 审核状态, 0-待审, 1-通过, 2-拒绝
                "visitStatus": 0,  // 访问状态, 0-私密, 1-公开
                "remark": null,
                "addTime": "2019-06-05T16:35:50",
                "updateTime": null,
                "userName": "管理员"  // 所属用户姓名
            }
        ]
    },
    "errmsg": "成功"
}      
error: 502, 504
```

#### 6.4 内容管理员对应列表查询  

```
url: 3002/biz/special/list/admin
method: GET
param: text
{
    name: "名称", 
    user: 1,  // 用户id
    auditStatus: 2,  // 审核状态, 0-待审, 1-通过, 2-拒绝
    visitStatus: 0,  // 访问状态, 0-私密, 1-公开
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
                "userId": 1,  // 所属用户id
                "name": "aaa",  // 标题
                "briefInfo": "111",  // 简介
                "detailInfo": null,  // 富文本详情
                "auditStatus": 0,  // 审核状态, 0-待审, 1-通过, 2-拒绝
                "visitStatus": 0,  // 访问状态, 0-私密, 1-公开
                "remark": null,
                "addTime": "2019-06-05T16:35:50",
                "updateTime": null,
                "userName": "管理员"  // 所属用户姓名
            }
        ]
    },
    "errmsg": "成功"
}      
error: 502, 504
```

#### 6.5 添加

```
url: 3002/biz/special/add
method: POST
param: json
{
    "userId": 1,  // 所属用户id
    "name": "aaa",  // 标题
    "briefInfo": "111",  // 简介
    "detailInfo": null,  // 富文本详情
    "auditStatus": 0,  // 审核状态, 0-待审, 1-通过, 2-拒绝
    "visitStatus": 0,  // 访问状态, 0-私密, 1-公开
    "remark": null
}
return: json
{
    "errno": 0,
    "data": {
        "id": 1,
        "userId": 1,  // 所属用户id
        "name": "aaa",  // 标题
        "briefInfo": "111",  // 简介
        "detailInfo": null,  // 富文本详情
        "auditStatus": 0,  // 审核状态, 0-待审, 1-通过, 2-拒绝
        "visitStatus": 0,  // 访问状态, 0-私密, 1-公开
        "remark": null,
        "addTime": "2019-06-05T16:35:50",
        "updateTime": null,
        "userName": "管理员"  // 所属用户姓名
    },
    "errmsg": "成功"
}      
error: 502, 503
```

#### 6.6 编辑

```
url: 3002/biz/special/edit
method: POST
param: json
{
    "id": 1,  // 主键 
    "userId": 1,  // 所属用户id
    "name": "aaa",  // 标题
    "briefInfo": "111",  // 简介
    "detailInfo": null,  // 富文本详情
    "auditStatus": 0,  // 审核状态, 0-待审, 1-通过, 2-拒绝
    "visitStatus": 0,  // 访问状态, 0-私密, 1-公开
    "remark": null
}
return: json
{
    "errno": 0,
    "data": {
        "id": 1,
        "userId": 1,  // 所属用户id
        "name": "aaa",  // 标题
        "briefInfo": "111",  // 简介
        "detailInfo": null,  // 富文本详情
        "auditStatus": 0,  // 审核状态, 0-待审, 1-通过, 2-拒绝
        "visitStatus": 0,  // 访问状态, 0-私密, 1-公开
        "remark": null,
        "addTime": "2019-06-05T16:35:50",
        "updateTime": null,
        "userName": "管理员"  // 所属用户姓名
    },
    "errmsg": "成功"
}      
error: 502, 503
```

#### 6.7 删除

```
url: 3002/biz/special/del
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

#### 6.8 简介审核

```
url: 3002/biz/special/audit
method: GET
param: text
{
    id: 1,  // 信息id
    auditStatus: 2,  // 审核状态, 0-待审, 1-通过, 2-拒绝
}
return: json
{
    "errno": 0,
    "errmsg": "成功"
}      
error: 502, 503, 507, 603
```
