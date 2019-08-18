# DB-NODE

## 数据库设计

### 1. 系统基础

#### 1.1 节点表(BEEN_NODE)
| column | type | name | is_null | default | remark |
| :--- | :---: | :---: | :---: | :---: | ---: |
| id | int(11) | 主键 | not null | - | 主键 |
| name        | varchar(20)  |      姓名      | not null |    -    |                  |
| gender      | smallint(6)  |      性别      | not null |    -    |                  |
| icon        | varchar(500) |      头像      |    -     |    -    |                  |
| birthday    |     date     |      生日      |    -     |    -    |                  |
| deathday    |     date     |    逝世日期    |    -     |    -    |                  |
| family_id   |   int(11)    |    族谱的id    |    -     |    -    |                  |
| description |     text     |    生平简介    |    -     |    -    |                  |
| father_node |  bigint(20)  |    父亲节点    |    -     |    -    |                  |
| mother_node |  bigint(20)  |    母亲节点    |    -     |    -    |                  |
| spouse_node |  bigint(20)  |    配偶节点    |    -     |    -    |                  |
| password    | varchar(16)  |      密码      |    -     |    -    |                  |
| code        |   char(24)   |     唯一码     | not null |    -    |                  |
| center      |  tinyint(4)  | 是否为中心节点 | not null |    0    |   1-是；0-不是； |
| deleted     |  tinyint(4)  |    逻辑删除    | not null |    0    | 0-正常, 1-已删除 |
| add_time    |   datetime   |    添加时间    | not null |         |                  |
| update_time |   datetime   |    修改时间    | not null |         |                  |

```
CREATE TABLE `been_node` (
  `id` int(20) NOT NULL AUTO_INCREMENT COMMENT 'ID',
  `name` varchar(20) CHARACTER SET utf8mb4 NOT NULL COMMENT '姓名',
  `gender` smallint(6) NOT NULL COMMENT '性别；',
  `icon` varchar(500) CHARACTER SET utf8mb4 DEFAULT NULL COMMENT '头像',
  `birthday` date DEFAULT NULL COMMENT '生日',
  `deathday` date DEFAULT NULL COMMENT '逝世日期',
  `family_id` int(11) NOT NULL COMMENT '族谱的id',
  `description` text COMMENT '生平简介',
  `father_node` bigint(20) DEFAULT NULL COMMENT '父亲节点',
  `mother_node` bigint(20) DEFAULT NULL COMMENT '母亲节点',
  `spouse_node` bigint(20) DEFAULT NULL COMMENT '配偶节点',
  `password` varchar(16) CHARACTER SET utf8mb4 DEFAULT NULL COMMENT '密码',
  `code` char(24) CHARACTER SET utf8mb4 NOT NULL COMMENT '唯一码',
  `center` tinyint(4) NOT NULL DEFAULT '0' COMMENT '是否为中心节点；1-是；0-不是；',
  `deleted` tinyint(4) NOT NULL DEFAULT '0' COMMENT '逻辑删除',
  `add_time` datetime NOT NULL DEFAULT CURRENT_TIMESTAMP COMMENT '添加时间',
  `update_time` datetime NOT NULL DEFAULT CURRENT_TIMESTAMP COMMENT '修改时间',
  PRIMARY KEY (`id`),
  UNIQUE KEY `唯一码` (`code`)
)ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_bin;
```

#### 1.2 媒体资源表(BEEN_MEDIA)
| column | type | name | is_null | default | remark |
| :--- | :---: | :---: | :---: | :---: | ---: |
| id | int(20) | 主键 | not null | - | 主键 |
| node_id     |   int(20)    | 对应节点id | not null |    -    |                         |
| media_url   | varchar(255) |  资源位置  | not null |    -    |                         |
| title       | varchar(255) |    标题    | not null |    -    |                         |
| time        | datetime(6)  |    时间    |    -     |    -    |                         |
| address     | varchar(255) |    地址    |    -     |    -    |                         |
| character   | varchar(255) |    人物    |    -     |    -    |                         |
| description | varchar(255) |    描述    |    -     |    -    |                         |
| type        |   int(10)    |    类型    | not null |    -    | 1：图片 2：视频 3：音频 |
| add_time    |   datetime   |  创建时间  | not null |    -    |                       - |
| update_time |   datetime   |  更新时间  |    -     |    -    | - |
| deleted | tinyint(1) | 逻辑删除 | not null | 0 | 0-正常, 1-已删除 |

```
CREATE TABLE `been_media` (
  `id` int(20) NOT NULL AUTO_INCREMENT,
  `node_id` int(20) NOT NULL COMMENT '用户id.',
  `media_url` varchar(255) CHARACTER SET utf8mb4 NOT NULL,
  `title` varchar(255) CHARACTER SET utf8mb4 NOT NULL,
  `time` datetime(6) NOT NULL,
  `address` varchar(255) CHARACTER SET utf8mb4 DEFAULT NULL,
  `character` varchar(255) CHARACTER SET utf8mb4 DEFAULT NULL,
  `description` varchar(255) CHARACTER SET utf8mb4 DEFAULT NULL,
  `type` int(10) NOT NULL COMMENT 'type 1：图片 2：视频 3：音频',
  `add_time` datetime(6) NOT NULL COMMENT '添加时间',
  `update_time` datetime(6) NOT NULL COMMENT '更新时间',
  `deleted` tinyint(1) unsigned zerofill NOT NULL COMMENT '0:存在\r\n1:删除',
  PRIMARY KEY (`id`),
  UNIQUE KEY `media_url` (`media_url`) USING BTREE
)ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_bin;
```


