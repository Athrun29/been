# BEEN-PEDIGREE

## 接口设计
 
### 1. 家谱管理

#### 1.1 查看详情

```
url: 3002/biz/pedigree/read/{id}
remark: 用于web端编辑查看
method: GET
param: 家谱节点id
return: json
{
    "errno": 0,
    "data": {
        "id": 1,
        "userId": 1,  // 用户id, 只有与用户有关联的节点有值
        "name": "姓名",
        "gender": 1,  // 性别, 0-未知, 1-男, 2-女
        "logoUrl": "头像地址",
        "briefInfo": "简介",
        "auditStatus": 1,  // 审核状态, 0-待审, 1-通过, 2-拒绝
        "spouseId": 1,  // 配偶节点id
        "remark": "备注",
        "addTime": "2019-06-27T15:25:00",
        "updateTime": "2019-06-27T15:25:00"
    },
    "errmsg": "成功"
}     
error: 502, 503, 507
```

#### 1.2 按家谱节点id查询展示

```
url: 3002/biz/pedigree/show/node/{id}
remark: 用于wap端调用展示
method: GET
param: 家谱节点id
return: json
{
    "errno": 0,
    "data": {
        "id": 1,
        "name": "姓名",
        "gender": 1,  // 性别, 0-未知, 1-男, 2-女
        "logoUrl": "头像地址",
        "briefInfo": "简介",
        "auditStatus": 1,  // 审核状态, 0-待审, 1-通过, 2-拒绝
        "spouseId": 1,  // 配偶节点id
        "remark": "备注",
        "addTime": "2019-06-27T15:25:00",
        "updateTime": "2019-06-27T15:25:00", 
        // --- 父辈节点
        "upperNodes": [
            {
                "id": 4,
                "name": "test_parent",
                "gender": 1,
                "logoUrl": "333",
                "briefInfo": "33333",
                "auditStatus": 1,
                "remark": null,
                "addTime": "2019-06-27T15:51:21",
                "updateTime": null
            }
        ],
        // --- 子女节点
        "lowerNodes": [
            {
                "id": 2,
                "name": "test_son",
                "gender": 1,
                "logoUrl": "111",
                "briefInfo": "111111",
                "auditStatus": 1,
                "remark": null,
                "addTime": "2019-06-27T15:49:32",
                "updateTime": null
            }
        ]
    },
    "errmsg": "成功"
}     
error: 502, 503, 507
```

#### 1.3 按用户id查询展示  

```
url: 3002/biz/pedigree/show/user/{id}
remark: 用于wap端调用展示
method: GET
param: 用户id
return: json
{
    "errno": 0,
    "data": {
        "id": 1,
        "userId": 1,  // 用户id, 只有与用户有关联的节点有值
        "name": "姓名",
        "gender": 1,  // 性别, 0-未知, 1-男, 2-女
        "logoUrl": "头像地址",
        "briefInfo": "简介",
        "auditStatus": 1,  // 审核状态, 0-待审, 1-通过, 2-拒绝
        "spouseId": 1,  // 配偶节点id
        "remark": "备注",
        "addTime": "2019-06-27T15:25:00",
        "updateTime": "2019-06-27T15:25:00", 
        // --- 父辈节点
        "upperNodes": [
            {
                "id": 4,
                "userId": null, 
                "name": "test_parent",
                "gender": 1,
                "logoUrl": "333",
                "briefInfo": "33333",
                "auditStatus": 1,
                "remark": null,
                "addTime": "2019-06-27T15:51:21",
                "updateTime": null
            }
        ],
        // --- 子女节点
        "lowerNodes": [
            {
                "id": 2,
                "userId": null, 
                "name": "test_son",
                "gender": 1,
                "logoUrl": "111",
                "briefInfo": "111111",
                "auditStatus": 1,
                "remark": null,
                "addTime": "2019-06-27T15:49:32",
                "updateTime": null
            }
        ]
    },
    "errmsg": "成功"
}     
error: 502, 503, 507
```

#### 1.4 家谱节点列表  

```
url: 3002/biz/pedigree/list
method: GET
param: text
{
    name: "姓名", 
    user: 1,  // 用户id
    auditStatus: 2,  // 审核状态, 0-待审, 1-通过, 2-拒绝
    relation: 1,  // 节点id, 传入该参数会把查询范围定位到与对应节点有关联的节点
    page: 1,    // 页数
    limit: 10,    // 每页容量
    sort: "update_time",    // 排序字段
    order: "desc",    // 排序规则
}
return: json
{
    "errno": 0,
    "data": {
        "total": 3,
        "items": [
            {
                "id": 1,
                "userId": 1,  // 用户id, 只有与用户有关联的节点有值
                "name": "姓名",
                "gender": 1,  // 性别, 0-未知, 1-男, 2-女
                "logoUrl": "头像地址",
                "briefInfo": "简介",
                "auditStatus": 1,  // 审核状态, 0-待审, 1-通过, 2-拒绝
                "spouseId": 1,  // 配偶节点id
                "remark": "备注",
                "addTime": "2019-06-27T15:25:00",
                "updateTime": "2019-06-27T15:25:00"
            }
        ]
    },
    "errmsg": "成功"
}     
error: 502, 504
```

#### 1.5 添加

```
url: 3002/biz/pedigree/add
method: POST
param: json
{
    "userId": 1,  // 用户id, 只有与用户有关联的节点有值
    "name": "姓名",
    "gender": 1,  // 性别, 0-未知, 1-男, 2-女
    "logoUrl": "头像地址",
    "briefInfo": "简介",  // 可选
    "remark": "备注"  // 可选
}
return: json
{
    "errno": 0,
    "data": {
        "id": 1,
        "userId": 1,  // 用户id, 只有与用户有关联的节点有值
        "name": "姓名",
        "gender": 1,  // 性别, 0-未知, 1-男, 2-女
        "logoUrl": "头像地址",
        "briefInfo": "简介",
        "auditStatus": 1,  // 审核状态, 0-待审, 1-通过, 2-拒绝
        "remark": null,
        "addTime": "2019-06-27T15:25:00",
        "updateTime": "2019-06-27T15:25:00"
    },
    "errmsg": "成功"
}      
error: 502, 503, 702
```

#### 1.6 编辑

```
url: 3002/biz/pedigree/edit
method: POST
param: json
{
    "id": 1,  // 家谱节点id
    "userId": 1,  // 用户id, 只有与用户有关联的节点有值
    "name": "姓名",
    "gender": 1,  // 性别, 0-未知, 1-男, 2-女
    "logoUrl": "头像地址",
    "briefInfo": "简介",  // 可选
    "remark": "备注"  // 可选
}
return: json
{
    "errno": 0,
    "data": {
        "id": 1,
        "userId": 1,  // 用户id, 只有与用户有关联的节点有值
        "name": "姓名",
        "gender": 1,  // 性别, 0-未知, 1-男, 2-女
        "logoUrl": "头像地址",
        "briefInfo": "简介",
        "auditStatus": 1,  // 审核状态, 0-待审, 1-通过, 2-拒绝
        "remark": null,
        "addTime": "2019-06-27T15:25:00",
        "updateTime": "2019-06-27T15:25:00"
    },
    "errmsg": "成功"
}      
error: 502, 503, 702
```

#### 1.7 删除

```
url: 3002/biz/pedigree/del
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

#### 1.8 查看某节点的父辈节点

```
url: 3002/biz/pedigree/upper/node/{id}
method: GET
param: 家谱节点id
return: json
{
    "errno": 0,
    "data": [
        {
            "id": 1,
            "userId": 1,  // 用户id, 只有与用户有关联的节点有值
            "name": "姓名",
            "gender": 1,  // 性别, 0-未知, 1-男, 2-女
            "logoUrl": "头像地址",
            "briefInfo": "简介",
            "auditStatus": 1,  // 审核状态, 0-待审, 1-通过, 2-拒绝
            "spouseId": 1,  // 配偶节点id
            "remark": null,
            "addTime": "2019-06-27T15:25:00",
            "updateTime": "2019-06-27T15:25:00"
        }
    ],
    "errmsg": "成功"
}     
error: 502, 503, 507
```

#### 1.9 查看某节点的子辈节点

```
url: 3002/biz/pedigree/lower/node/{id}
method: GET
param: 家谱节点id
return: json
{
    "errno": 0,
    "data": [
        {
            "id": 1,
            "userId": 1,  // 用户id, 只有与用户有关联的节点有值
            "name": "姓名",
            "gender": 1,  // 性别, 0-未知, 1-男, 2-女
            "logoUrl": "头像地址",
            "briefInfo": "简介",
            "auditStatus": 1,  // 审核状态, 0-待审, 1-通过, 2-拒绝
            "spouseId": 1,  // 配偶节点id
            "remark": "备注",
            "addTime": "2019-06-27T15:25:00",
            "updateTime": "2019-06-27T15:25:00"
        }
    ],
    "errmsg": "成功"
}     
error: 502, 503, 507
```

#### 1.10 添加父辈新节点

```
url: 3002/biz/pedigree/upper/add
method: POST
param: json
{
    "node": 1,  // 家谱节点id
    "userId": 1,  // 用户id, 可选
    "name": "姓名",
    "gender": 1,  // 性别, 0-未知, 1-男, 2-女
    "logoUrl": "头像地址",
    "briefInfo": "简介",  // 可选
    "remark": "备注"  // 可选
}
return: json
{
    "errno": 0,
    "data": {
        "id": 1,
        "userId": 1,  // 用户id, 只有与用户有关联的节点有值
        "name": "姓名",
        "gender": 1,  // 性别, 0-未知, 1-男, 2-女
        "logoUrl": "头像地址",
        "briefInfo": "简介",
        "auditStatus": 1,  // 审核状态, 0-待审, 1-通过, 2-拒绝
        "spouseId": 1,  // 配偶节点id
        "remark": null,
        "addTime": "2019-06-27T15:25:00",
        "updateTime": "2019-06-27T15:25:00"
    },
    "errmsg": "成功"
}      
error: 502, 503, 702
```

#### 1.11 添加子辈新节点

```
url: 3002/biz/pedigree/lower/add
method: POST
param: json
{
    "node": 1,  // 家谱节点id
    "userId": 1,  // 用户id, 可选
    "name": "姓名",
    "gender": 1,  // 性别, 0-未知, 1-男, 2-女
    "logoUrl": "头像地址",
    "briefInfo": "简介",  // 可选
    "remark": "备注"  // 可选
}
return: json
{
    "errno": 0,
    "data": {
        "id": 1,
        "userId": 1,  // 用户id, 只有与用户有关联的节点有值
        "name": "姓名",
        "gender": 1,  // 性别, 0-未知, 1-男, 2-女
        "logoUrl": "头像地址",
        "briefInfo": "简介",
        "auditStatus": 1,  // 审核状态, 0-待审, 1-通过, 2-拒绝
        "spouseId": 1,  // 配偶节点id
        "remark": null,
        "addTime": "2019-06-27T15:25:00",
        "updateTime": "2019-06-27T15:25:00"
    },
    "errmsg": "成功"
}      
error: 502, 503, 702
```

#### 1.12 向父辈中添加已有节点

```
url: 3002/biz/pedigree/upper/attach
remark: 向主节点baseNode的父辈中加入attachNode, 同时向attachNode的子辈中加入baseNode
method: POST
param: json
{
    "baseNode": 1,  // 主节点id
    "attachNode": 1  // 被添加节点id
}
return: json
{
    "errno": 0,
    "data": {
        "id": 1,
        "userId": 1,  // 用户id, 只有与用户有关联的节点有值
        "name": "姓名",
        "gender": 1,  // 性别, 0-未知, 1-男, 2-女
        "logoUrl": "头像地址",
        "briefInfo": "简介",
        "auditStatus": 1,  // 审核状态, 0-待审, 1-通过, 2-拒绝
        "spouseId": 1,  // 配偶节点id
        "remark": null,
        "addTime": "2019-06-27T15:25:00",
        "updateTime": "2019-06-27T15:25:00"
    },
    "errmsg": "成功"
}      
error: 502, 503, 703
```

#### 1.13 向子辈添加已有节点

```
url: 3002/biz/pedigree/lower/attach
remark: 向主节点baseNode的子辈中加入attachNode, 同时向attachNode的父辈中加入baseNode
method: POST
param: json
{
    "baseNode": 1,  // 主节点id
    "attachNode": 1  // 被添加节点id
}
return: json
{
    "errno": 0,
    "data": {
        "id": 1,
        "userId": 1,  // 用户id, 只有与用户有关联的节点有值
        "name": "姓名",
        "gender": 1,  // 性别, 0-未知, 1-男, 2-女
        "logoUrl": "头像地址",
        "briefInfo": "简介",
        "auditStatus": 1,  // 审核状态, 0-待审, 1-通过, 2-拒绝
        "spouseId": 1,  // 配偶节点id
        "remark": null,
        "addTime": "2019-06-27T15:25:00",
        "updateTime": "2019-06-27T15:25:00"
    },
    "errmsg": "成功"
}      
error: 502, 503, 703
```

#### 1.14 移除父辈中节点

```
url: 3002/biz/pedigree/upper/remove
remark: 主节点baseNode的父辈中移除attachNode, 同时attachNode的子辈中移除baseNode
method: POST
param: json
{
    "baseNode": 1,  // 主节点id
    "attachNode": 1  // 被移除节点id
}
return: json
{
    "errno": 0,
    "errmsg": "成功"
}      
error: 502, 503
```

#### 1.15 移除子辈中节点

```
url: 3002/biz/pedigree/lower/remove
remark: 主节点baseNode的子辈中移除attachNode, 同时attachNode的父辈中移除baseNode
method: POST
param: json
{
    "baseNode": 1,  // 主节点id
    "attachNode": 1  // 被移除节点id
}
return: json
{
    "errno": 0,
    "errmsg": "成功"
}      
error: 502, 503
```

#### 1.16 查看配偶节点

```
url: 3002/biz/pedigree/spouse/node/{id}
method: GET
param: 家谱节点id
return: json
{
    "errno": 0,
    "data": {
        "id": 6,
        "userId": null,
        "name": "test_spouse",
        "gender": 2,
        "logoUrl": "444",
        "briefInfo": "44444",
        "auditStatus": 1,
        "spouseId": 1,
        "remark": null,
        "addTime": "2019-06-30T16:33:55",
        "updateTime": null
    },
    "errmsg": "成功"
}     
error: 502, 503, 507
```

#### 1.17 添加配偶新节点
```
url: 3002/biz/pedigree/spouse/add
method: POST
param: json
{
    "node": 1,  // 家谱节点id
    "userId": 1,  // 用户id, 可选
    "name": "姓名",
    "gender": 1,  // 性别, 0-未知, 1-男, 2-女
    "logoUrl": "头像地址",
    "briefInfo": "简介",  // 可选
    "remark": "备注"  // 可选
}
return: json
{
    "errno": 0,
    "data": {
        "id": 1,
        "userId": 1,  // 用户id, 只有与用户有关联的节点有值
        "name": "姓名",
        "gender": 1,  // 性别, 0-未知, 1-男, 2-女
        "logoUrl": "头像地址",
        "briefInfo": "简介",
        "auditStatus": 1,  // 审核状态, 0-待审, 1-通过, 2-拒绝
        "spouseId": 1,  // 配偶节点id
        "remark": null,
        "addTime": "2019-06-27T15:25:00",
        "updateTime": "2019-06-27T15:25:00"
    },
    "errmsg": "成功"
}      
error: 502, 503, 702, 705
```

#### 1.18 添加已有节点作配偶节点

```
url: 3002/biz/pedigree/spouse/attach
remark: 主节点baseNode的配偶设为attachNode, 同时attachNode的配偶设为baseNode
method: POST
param: json
{
    "baseNode": 1,  // 主节点id
    "attachNode": 1  // 被添加节点id
}
return: json
{
    "errno": 0,
    "data": {
        "id": 1,
        "userId": 1,  // 用户id, 只有与用户有关联的节点有值
        "name": "姓名",
        "gender": 1,  // 性别, 0-未知, 1-男, 2-女
        "logoUrl": "头像地址",
        "briefInfo": "简介",
        "auditStatus": 1,  // 审核状态, 0-待审, 1-通过, 2-拒绝
        "spouseId": 1,  // 配偶节点id
        "remark": null,
        "addTime": "2019-06-27T15:25:00",
        "updateTime": "2019-06-27T15:25:00"
    },
    "errmsg": "成功"
}      
error: 502, 503, 705, 706
```

#### 1.19 移除配偶节点

```
url: 3002/biz/pedigree/lower/remove
remark: 主节点baseNode的配偶设为null, 同时attachNode的配偶设为null
method: POST
param: json
{
    "baseNode": 1,  // 主节点id
    "attachNode": 1  // 被移除节点id
}
return: json
{
    "errno": 0,
    "errmsg": "成功"
}      
error: 502, 503, 707
```

#### 1.20 按家谱节点id预览完整关系

```
url: 3002/biz/pedigree/preview/node/{id}
remark: 用于web端调用预览
method: GET
param: 家谱节点id
return: json
{
    "errno": 0,
    "data": {
        "id": 1,
        "name": "姓名",
        "gender": 1,  // 性别, 0-未知, 1-男, 2-女
        "logoUrl": "头像地址",
        "briefInfo": "简介",
        "auditStatus": 1,  // 审核状态, 0-待审, 1-通过, 2-拒绝
        "spouseId": 1,  // 配偶节点id
        "remark": "备注",
        "addTime": "2019-06-27T15:25:00",
        "updateTime": "2019-06-27T15:25:00", 
        // --- 父辈节点
        "upperNodes": [
            {
                "id": 4,
                "name": "test_parent",
                "gender": 1,
                "logoUrl": "333",
                "briefInfo": "33333",
                "auditStatus": 1,
                "remark": null,
                "addTime": "2019-06-27T15:51:21",
                "updateTime": null
            }
        ],
        // --- 子女节点
        "lowerNodes": [
            {
                "id": 2,
                "name": "test_son",
                "gender": 1,
                "logoUrl": "111",
                "briefInfo": "111111",
                "auditStatus": 1,
                "remark": null,
                "addTime": "2019-06-27T15:49:32",
                "updateTime": null
            }
        ]
    },
    "errmsg": "成功"
}     
error: 502, 503, 507
```

#### 1.21 按用户id预览完整关系

```
url: 3002/biz/pedigree/preview/user/{id}
remark: 用于web端调用预览
method: GET
param: 用户id
return: json
{
    "errno": 0,
    "data": {
        "id": 1,
        "name": "姓名",
        "gender": 1,  // 性别, 0-未知, 1-男, 2-女
        "logoUrl": "头像地址",
        "briefInfo": "简介",
        "auditStatus": 1,  // 审核状态, 0-待审, 1-通过, 2-拒绝
        "spouseId": 1,  // 配偶节点id
        "remark": "备注",
        "addTime": "2019-06-27T15:25:00",
        "updateTime": "2019-06-27T15:25:00", 
        // --- 父辈节点
        "upperNodes": [
            {
                "id": 4,
                "name": "test_parent",
                "gender": 1,
                "logoUrl": "333",
                "briefInfo": "33333",
                "auditStatus": 1,
                "remark": null,
                "addTime": "2019-06-27T15:51:21",
                "updateTime": null
            }
        ],
        // --- 子女节点
        "lowerNodes": [
            {
                "id": 2,
                "name": "test_son",
                "gender": 1,
                "logoUrl": "111",
                "briefInfo": "111111",
                "auditStatus": 1,
                "remark": null,
                "addTime": "2019-06-27T15:49:32",
                "updateTime": null
            }
        ]
    },
    "errmsg": "成功"
}     
error: 502, 503, 507
```

#### 1.22 家谱节点审核

```
url: 3002/biz/pedigree/audit
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
error: 502, 503, 507, 704
```
