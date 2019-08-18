# BEEN-NODE

## 接口设计

### 1. 节点管理

#### 1.1 查看单个节点详情

```
url: 3002/biz/node/read/{1}
method: GET
param: param	id=节点id
return: json
{
    "errno": 0,
    "data": {
        "id": 1,
        "name": "测试B",
        "gender": 0,
        "icon": "sdfbtrsne",
        "birthday": "2019-04-30",
        "deathday": null,
        "familyId": 1,
        "fatherNode": null,
        "motherNode": null,
        "spouseNode": null,
        "password": null,
        "code": "zdfstsvtr",
        "center": false,
        "deleted": false,
        "addTime": "2019-05-20T17:11:47",
        "updateTime": "2019-05-20T17:40:12",
        "description": "qwe",
        "photosList": [
            {
                "id": 1,
                "nodeId": 1,
                "mediaUrl": "qwe",
                "title": "qwe",
                "time": "2019-05-20T18:16:30",
                "address": "qwe",
                "character": "qwe",
                "description": "qwe",
                "type": 1,
                "addTime": "2019-05-15T18:16:47",
                "updateTime": "2019-05-20T18:16:50",
                "deleted": false
            },
            {
                "id": 5,
                "nodeId": 1,
                "mediaUrl": "http://shangdaochuancheng.oss-cn-beijing.aliyuncs.com/photo/admin-20190522-2f0561c3476745d1ab3d2ee13fca70d9.jpg",
                "title": "42.jpg",
                "time": "2019-05-22T00:05:02.567",
                "address": null,
                "character": null,
                "description": null,
                "type": 1,
                "addTime": "2019-05-22T00:05:02.567",
                "updateTime": "2019-05-22T00:05:02.567",
                "deleted": false
            },
            {
                "id": 6,
                "nodeId": 1,
                "mediaUrl": "http://shangdaochuancheng.oss-cn-beijing.aliyuncs.com/photo/admin-20190522-f2ddb841c06b4499bc1c8305ec5de352.jpg",
                "title": "42.jpg",
                "time": "2019-05-22T00:12:06.967",
                "address": null,
                "character": null,
                "description": null,
                "type": 1,
                "addTime": "2019-05-22T00:12:06.966",
                "updateTime": "2019-05-22T00:12:06.966",
                "deleted": false
            },
            {
                "id": 7,
                "nodeId": 1,
                "mediaUrl": "http://shangdaochuancheng.oss-cn-beijing.aliyuncs.com/photo/admin-20190522-e23effaf03ca49b0bf4ba1f0efba8673.jpg",
                "title": "52f6ef417376c.jpg",
                "time": "2019-05-22T00:12:13.519",
                "address": null,
                "character": null,
                "description": null,
                "type": 1,
                "addTime": "2019-05-22T00:12:13.519",
                "updateTime": "2019-05-22T00:12:13.519",
                "deleted": false
            },
            {
                "id": 8,
                "nodeId": 1,
                "mediaUrl": "http://shangdaochuancheng.oss-cn-beijing.aliyuncs.com/photo/admin-20190522-b66e4d673e604b6e91b50c30cbd5523e.jpg",
                "title": "55cb204d7e26a.jpg",
                "time": "2019-05-22T00:12:21.223",
                "address": null,
                "character": null,
                "description": null,
                "type": 1,
                "addTime": "2019-05-22T00:12:21.223",
                "updateTime": "2019-05-22T00:12:21.223",
                "deleted": false
            }
        ],
        "musicsList": [
            {
                "id": 2,
                "nodeId": 1,
                "mediaUrl": "wdsdf",
                "title": "sgrd",
                "time": "2019-05-07T18:17:04",
                "address": "dbtv",
                "character": "d",
                "description": "dtb",
                "type": 2,
                "addTime": "2019-05-20T18:17:12",
                "updateTime": "2019-05-20T18:17:15",
                "deleted": false
            },
            {
                "id": 4,
                "nodeId": 1,
                "mediaUrl": "http://shangdaochuancheng.oss-cn-beijing.aliyuncs.com/photo/admin-20190521-0bc2d5d2924e41e39f1f640c6b979e4d.jpg",
                "title": "42.jpg",
                "time": "2019-05-21T09:45:17.044",
                "address": null,
                "character": null,
                "description": null,
                "type": 2,
                "addTime": "2019-05-21T09:45:17.043",
                "updateTime": "2019-05-21T09:45:17.044",
                "deleted": false
            }
        ],
        "videosList": [
            {
                "id": 3,
                "nodeId": 1,
                "mediaUrl": "hhh",
                "title": "42.jpg",
                "time": "2019-05-21T09:44:02.286",
                "address": null,
                "character": null,
                "description": null,
                "type": 3,
                "addTime": "2019-05-21T09:44:02.286",
                "updateTime": "2019-05-21T09:44:02.286",
                "deleted": false
            }
        ]
    },
    "errmsg": "成功"
}
```

#### 1.2 修改单个节点

```
url: 3002/biz/node/edit
method: POST
param: json
{
    "id": 1,
    "name": "测试B",
    "gender": 0,
    "icon": "sdfbtrsne",
    "birthday": "2019-04-30",
    "deathday": null,
    "familyId": 1,
    "fatherNode": null,
    "motherNode": null,
    "spouseNode": null,
    "password": null,
    "code": "zdfstsvtr",
    "center": false,
    "deleted": false,
    "addTime": "2019-05-20T17:11:47",
    "description": "qwe"
}
return: json
{
    "id": 1,
    "name": "测试A",
    "gender": 1,
    "icon": "qwe",
    "birthday": "2019-04-30",
    "deathday": null,
    "familyId": 1,
    "fatherNode": null,
    "motherNode": null,
    "spouseNode": null,
    "password": null,
    "code": "123qwe",
    "center": false,
    "deleted": false,
    "addTime": "2019-05-20T17:11:47",
    "updateTime": "2019-05-20T17:11:47",
    "description": "qwe"
}
```

#### 1.3 添加节点

```
url: 3002/biz/node/add
method: POST
param: json
{
    "name": "测试B",
    "gender": 0,
    "icon": "sdfbtrsne",
    "birthday": "2019-04-30",
    "deathday": null,
    "familyId": 1,
    "fatherNode": null,
    "motherNode": null,
    "spouseNode": null,
    "password": null,
    "code": "zdfstsvtr",
    "center": false,
    "deleted": false,
    "description": "qwe"
}
return: json
{
    "id": 11,
    "name": "测试B",
    "gender": 0,
    "icon": "sdfbtrsne",
    "birthday": "2019-04-30",
    "deathday": null,
    "familyId": 1,
    "fatherNode": null,
    "motherNode": null,
    "spouseNode": null,
    "password": null,
    "code": "vzsclnsc2anrye55rjk1c7yo",
    "center": false,
    "deleted": false,
    "addTime": "2019-05-20T17:52:01",
    "updateTime": "2019-05-20T17:52:01",
    "description": "qwe"
}
```

#### 1.4 删除节点

```
url: 3002/biz/node/del
method: GET
param: param	ids=节点id
return: json
{
    {
    "errno": 0,
    "data": {
        "id": 1,
        "name": "测试A",
        "gender": 1,
        "icon": "qwe",
        "birthday": "2019-04-30",
        "deathday": null,
        "familyId": 1,
        "fatherNode": null,
        "motherNode": null,
        "spouseNode": null,
        "password": null,
        "code": "123qwe",
        "center": false,
        "deleted": false,
        "addTime": "2019-05-20T17:11:47",
        "updateTime": "2019-05-20T17:11:47",
        "description": "qwe"
    },
    "errmsg": "成功"
}
}      
error: 502, 510, 201
```

#### 1.5 查看节点列表

```
url: 3002/biz/node/list
method: GET
param: param	
{
	"name":"名字（搜索的关键词）"，
	"page":"页码"，
	"limit":"每页页数"，
	"sort":"排序字段"，
	"order":"排序方式，升序，降序"，
	"con":"其他条件"
}
return: json
{
    "errno": 0,
    "data": {
        "id": 1,
        "name": "测试A",
        "gender": 1,
        "icon": "qwe",
        "birthday": "2019-04-30",
        "deathday": null,
        "familyId": 1,
        "fatherNode": null,
        "motherNode": null,
        "spouseNode": null,
        "password": null,
        "code": "123qwe",
        "center": false,
        "deleted": false,
        "addTime": "2019-05-20T17:11:47",
        "updateTime": "2019-05-20T17:11:47",
        "description": "qwe"
    },
    "errmsg": "成功"
}

```





### 2. 多媒体管理

#### 2.1 单个图片上传

```
url: 3003/file/oss/uploadPhoto
method: POST
param: MultipartFile
return: json
{
    "errno": 0,
    "errmsg": "成功",
    "data":"url"//图片地址
}
```

#### 2.2 单个视频上传

```
url: 3003/file/oss/uploadVideo
method: POST
param: MultipartFile
return: json
{
    "errno": 0,
    "errmsg": "成功",
    "data":"url"
}
```

#### 2.3 单个音频上传

```
url: 3003/file/oss/uploadMusic
method: POST
param: MultipartFile
return: json
{
    "errno": 0,
    "data": "http://shangdaochuancheng.oss-cn-beijing.aliyuncs.com/video/admin-20190522-bed18406d589468192de1bc1bda663fe.mp3",
    "errmsg": "成功"
}
```

#### 2.4 节点上传图片，可批量

```
url: 3003/file/oss/uploadNodePhoto
method: POST
param: 
{
	"files":"MultipartFile[]"，
	"nodeId":"节点的id"
}
return: json
{
    [
    {
        "id": 9,
        "nodeId": 1,
        "mediaUrl": "http://shangdaochuancheng.oss-cn-beijing.aliyuncs.com/photo/admin-20190526-9327e082919e478ca882791302de61c9.jpg",
        "title": "42.jpg",
        "time": "2019-05-26T23:12:18.036",
        "address": null,
        "character": null,
        "description": null,
        "type": 1,
        "addTime": "2019-05-26T23:12:18.035",
        "updateTime": "2019-05-26T23:12:18.036",
        "deleted": false
    },
    {
        "id": 10,
        "nodeId": 1,
        "mediaUrl": "http://shangdaochuancheng.oss-cn-beijing.aliyuncs.com/photo/admin-20190526-16c61894e67044d2aedd92f20abf2537.jpg",
        "title": "52f6ef417376c.jpg",
        "time": "2019-05-26T23:12:21.586",
        "address": null,
        "character": null,
        "description": null,
        "type": 1,
        "addTime": "2019-05-26T23:12:21.586",
        "updateTime": "2019-05-26T23:12:21.586",
        "deleted": false
    }
	]
}
```

#### 2.5 节点上传音频，可批量

```
url: 3003/file/oss/uploadNodeMusic
method: POST
param: 
{
	"files":"MultipartFile[]"，
	"nodeId":"节点的id"
}
return: json
{
    [
    {
        "id": 9,
        "nodeId": 1,
        "mediaUrl": "http://shangdaochuancheng.oss-cn-beijing.aliyuncs.com/photo/admin-20190526-9327e082919e478ca882791302de61c9.jpg",
        "title": "42.jpg",
        "time": "2019-05-26T23:12:18.036",
        "address": null,
        "character": null,
        "description": null,
        "type": 1,
        "addTime": "2019-05-26T23:12:18.035",
        "updateTime": "2019-05-26T23:12:18.036",
        "deleted": false
    },
    {
        "id": 10,
        "nodeId": 1,
        "mediaUrl": "http://shangdaochuancheng.oss-cn-beijing.aliyuncs.com/photo/admin-20190526-16c61894e67044d2aedd92f20abf2537.jpg",
        "title": "52f6ef417376c.jpg",
        "time": "2019-05-26T23:12:21.586",
        "address": null,
        "character": null,
        "description": null,
        "type": 1,
        "addTime": "2019-05-26T23:12:21.586",
        "updateTime": "2019-05-26T23:12:21.586",
        "deleted": false
    }
	]
}
```

#### 2.6 节点上传视频，可批量

```
url: 3003/file/oss/uploadNodeVideo
method: POST
param: 
{
	"files":"MultipartFile[]"，
	"nodeId":"节点的id"
}
return: json
{
    [
    {
        "id": 9,
        "nodeId": 1,
        "mediaUrl": "http://shangdaochuancheng.oss-cn-beijing.aliyuncs.com/photo/admin-20190526-9327e082919e478ca882791302de61c9.jpg",
        "title": "42.jpg",
        "time": "2019-05-26T23:12:18.036",
        "address": null,
        "character": null,
        "description": null,
        "type": 1,
        "addTime": "2019-05-26T23:12:18.035",
        "updateTime": "2019-05-26T23:12:18.036",
        "deleted": false
    },
    {
        "id": 10,
        "nodeId": 1,
        "mediaUrl": "http://shangdaochuancheng.oss-cn-beijing.aliyuncs.com/photo/admin-20190526-16c61894e67044d2aedd92f20abf2537.jpg",
        "title": "52f6ef417376c.jpg",
        "time": "2019-05-26T23:12:21.586",
        "address": null,
        "character": null,
        "description": null,
        "type": 1,
        "addTime": "2019-05-26T23:12:21.586",
        "updateTime": "2019-05-26T23:12:21.586",
        "deleted": false
    }
	]
}
```

