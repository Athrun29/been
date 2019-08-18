# DB-BIZ

## 数据库设计

### 1. 模块管理

#### 1.1 模块表(BEEN_MODULE)
| column | type | name | is_null | default | remark |
| :--- | :---: | :---: | :---: | :---: | ---: |
| id | int(11) | 主键 | not null | - | 主键 |
| user_id | int(11) | 所属用户 | not null | - | - |
| name | varchar(255) | 名称 | not null | - | - |
| type | int(1) | 模块类型 | not null | - | 0-相册, 2-时间轴, 3-生平 |
| auth_status | int(1) | 访问状态 | not null | 0 | 0-私密, 1-密码访问, 2-公开 |
| audit_status | int(1) | 审核状态 | not null | 0 | 0-待审, 1-通过, 2-拒绝 |
| sort | int(1) | 顺序号 | not null | - | - |
| remark | varchar(63) | 备注 | - | - | - |
| add_time | datetime | 创建时间 | not null | - | - |
| update_time | datetime | 更新时间 | - | - | - |
| deleted | tinyint(1) | 逻辑删除 | not null | 0 | 0-正常, 1-已删除 |

```
CREATE TABLE `been_module` (
  `id` int(11) NOT NULL AUTO_INCREMENT,
  `user_id` int(11) NOT NULL COMMENT '用户',
  `name` varchar(255) COLLATE utf8mb4_bin NOT NULL COMMENT '名称',
  `type` int(1) NOT NULL COMMENT '类型, 0-相册, 2-时间轴, 3-生平',
  `auth_status` int(1) NOT NULL DEFAULT '0' COMMENT '授权状态, 0-私密, 1-密码访问, 2-公开',
  `audit_status` int(1) NOT NULL DEFAULT '0' COMMENT '审核状态, 0-待审核, 1-审核通过, 2-审核拒绝',
  `sort` int(100) NOT NULL COMMENT '顺序号',
  `remark` varchar(255) COLLATE utf8mb4_bin DEFAULT NULL COMMENT '备注',
  `add_time` datetime NOT NULL COMMENT '创建时间',
  `update_time` datetime DEFAULT NULL COMMENT '更新时间',
  `deleted` tinyint(1) NOT NULL DEFAULT '0' COMMENT '逻辑删除',
  PRIMARY KEY (`id`) USING BTREE
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_bin;
```

#### 1.2 影集表(BEEN_ALBUM)
| column | type | name | is_null | default | remark |
| :--- | :---: | :---: | :---: | :---: | ---: |
| id | int(11) | 主键 | not null | - | 主键 |
| user_id | int(11) | 所属用户 | not null | - | - |
| module_id | int(11) | 所属模块 | not null | - | - |
| name | varchar(255) | 名称 | not null | - | - |
| media_url | varchar(255) | 影像url | not null | - | - |
| type | int(1) | 类型 | not null | 0 | 0-照片, 1-视频, 2-音频 |
| mark_time | datetime | 时间 | - | - | - |
| mark_addr | varchar(255) | 地点 | - | - | - |
| mark_person | varchar(255) | 人物 | - | - | - |
| brief_info | varchar(255) | 简介 | - | - | - |
| sort | int(1) | 顺序号 | not null | 0 | - |
| remark | varchar(63) | 备注 | - | - | - |
| add_time | datetime | 创建时间 | not null | - | - |
| update_time | datetime | 更新时间 | - | - | - |
| deleted | tinyint(1) | 逻辑删除 | not null | 0 | 0-正常, 1-已删除 |

```
CREATE TABLE `been_album` (
  `id` int(11) NOT NULL AUTO_INCREMENT,
  `user_id` int(11) NOT NULL COMMENT '用户',
  `module_id` int(11) NOT NULL COMMENT '模块id',
  `name` varchar(255) COLLATE utf8mb4_bin NOT NULL COMMENT '名称',
  `media_url` varchar(255) COLLATE utf8mb4_bin NOT NULL COMMENT '影像url',
  `type` int(1) NOT NULL DEFAULT '0' COMMENT '类型, 0-照片, 1-视频, 2-音频',
  `mark_time` datetime DEFAULT NULL COMMENT '拍摄时间',
  `mark_addr` varchar(255) COLLATE utf8mb4_bin DEFAULT NULL COMMENT '拍摄地点',
  `mark_person` varchar(255) COLLATE utf8mb4_bin DEFAULT NULL COMMENT '拍摄人物',
  `brief_info` varchar(255) COLLATE utf8mb4_bin DEFAULT NULL COMMENT '简介',
  `sort` int(100) NOT NULL DEFAULT '0' COMMENT '顺序号',
  `remark` varchar(255) COLLATE utf8mb4_bin DEFAULT NULL COMMENT '备注',
  `add_time` datetime NOT NULL COMMENT '创建时间',
  `update_time` datetime DEFAULT NULL COMMENT '更新时间',
  `deleted` tinyint(1) NOT NULL DEFAULT '0' COMMENT '逻辑删除',
  PRIMARY KEY (`id`) USING BTREE
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_bin;
```

#### 1.3 时间轴表(BEEN_TIMELINE)
| column | type | name | is_null | default | remark |
| :--- | :---: | :---: | :---: | :---: | ---: |
| id | int(11) | 主键 | not null | - | 主键 |
| user_id | int(11) | 所属用户 | not null | - | - |
| module_id | int(11) | 所属模块 | not null | - | - |
| name | varchar(255) | 名称 | not null | - | - |
| mark_time | datetime | 标记时间 | not null | - | - |
| media_url | varchar(255) | 影像url | not null | - | - |
| brief_info | varchar(255) | 简介 | - | - | - |
| detail_info | text | 详情 | - | - | - |
| sort | int(1) | 顺序号 | not null | - | - |
| remark | varchar(63) | 备注 | - | - | - |
| add_time | datetime | 创建时间 | not null | - | - |
| update_time | datetime | 更新时间 | - | - | - |
| deleted | tinyint(1) | 逻辑删除 | not null | 0 | 0-正常, 1-已删除 |

```
CREATE TABLE `been_timeline` (
  `id` int(11) NOT NULL AUTO_INCREMENT,
  `user_id` int(11) NOT NULL COMMENT '用户',
  `module_id` int(11) NOT NULL COMMENT '模块id',
  `name` varchar(255) COLLATE utf8mb4_bin NOT NULL COMMENT '名称',
  `mark_time` datetime NOT NULL COMMENT '标记时间',
  `media_url` varchar(255) COLLATE utf8mb4_bin NOT NULL COMMENT '影像url',
  `brief_info` varchar(255) COLLATE utf8mb4_bin DEFAULT NULL COMMENT '简介',
  `detail_info` text COLLATE utf8mb4_bin COMMENT '详情',
  `sort` int(100) NOT NULL COMMENT '顺序号',
  `remark` varchar(255) COLLATE utf8mb4_bin DEFAULT NULL COMMENT '备注',
  `add_time` datetime NOT NULL COMMENT '创建时间',
  `update_time` datetime DEFAULT NULL COMMENT '更新时间',
  `deleted` tinyint(1) NOT NULL DEFAULT '0' COMMENT '逻辑删除',
  PRIMARY KEY (`id`) USING BTREE
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_bin;
```

#### 1.4 生平事件表(BEEN_EVENT)
| column | type | name | is_null | default | remark |
| :--- | :---: | :---: | :---: | :---: | ---: |
| id | int(11) | 主键 | not null | - | 主键 |
| user_id | int(11) | 所属用户 | not null | - | - |
| module_id | int(11) | 所属模块 | not null | - | - |
| name | varchar(255) | 名称 | not null | - | - |
| media_url | varchar(255) | 影像url | not null | - | - |
| brief_info | varchar(255) | 简介 | - | - | - |
| detail_info | text | 详情 | - | - | - |
| sort | int(1) | 顺序号 | not null | - | - |
| remark | varchar(63) | 备注 | - | - | - |
| add_time | datetime | 创建时间 | not null | - | - |
| update_time | datetime | 更新时间 | - | - | - |
| deleted | tinyint(1) | 逻辑删除 | not null | 0 | 0-正常, 1-已删除 |

```
CREATE TABLE `been_event` (
  `id` int(11) NOT NULL AUTO_INCREMENT,
  `user_id` int(11) NOT NULL COMMENT '用户',
  `module_id` int(11) NOT NULL COMMENT '模块id',
  `name` varchar(255) COLLATE utf8mb4_bin NOT NULL COMMENT '名称',
  `media_url` varchar(255) COLLATE utf8mb4_bin NOT NULL COMMENT '影像url',
  `brief_info` varchar(255) COLLATE utf8mb4_bin DEFAULT NULL COMMENT '简介',
  `detail_info` text COLLATE utf8mb4_bin COMMENT '详情',
  `sort` int(100) NOT NULL COMMENT '顺序号',
  `remark` varchar(255) COLLATE utf8mb4_bin DEFAULT NULL COMMENT '备注',
  `add_time` datetime NOT NULL COMMENT '创建时间',
  `update_time` datetime DEFAULT NULL COMMENT '更新时间',
  `deleted` tinyint(1) NOT NULL DEFAULT '0' COMMENT '逻辑删除',
  PRIMARY KEY (`id`) USING BTREE
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_bin;
```

#### 1.5 生平简介表(BEEN_INTRO)
| column | type | name | is_null | default | remark |
| :--- | :---: | :---: | :---: | :---: | ---: |
| id | int(11) | 主键 | not null | - | 主键 |
| user_id | int(11) | 所属用户 | not null | - | - |
| name | varchar(255) | 名称 | not null | - | - |
| motto | varchar(255) | 座右铭 | - | - | - |
| brief_info | varchar(255) | 简介 | - | - | - |
| detail_info | text | 详情 | - | - | - |
| audit_status | int(1) | 审核状态 | not null | 0 | 0-待审, 1-通过, 2-拒绝 |
| remark | varchar(63) | 备注 | - | - | - |
| add_time | datetime | 创建时间 | not null | - | - |
| update_time | datetime | 更新时间 | - | - | - |
| deleted | tinyint(1) | 逻辑删除 | not null | 0 | 0-正常, 1-已删除 |

```
CREATE TABLE `been_intro` (
  `id` int(11) NOT NULL AUTO_INCREMENT,
  `user_id` int(11) NOT NULL COMMENT '用户',
  `name` varchar(255) COLLATE utf8mb4_bin NOT NULL COMMENT '名称',
  `motto` varchar(255) COLLATE utf8mb4_bin NOT NULL COMMENT '座右铭',
  `brief_info` varchar(255) COLLATE utf8mb4_bin DEFAULT NULL COMMENT '简介',
  `detail_info` text COLLATE utf8mb4_bin COMMENT '详情',
  `audit_status` int(1) NOT NULL DEFAULT '0' COMMENT '审核状态, 0-待审核, 1-审核通过, 2-审核拒绝',
  `remark` varchar(255) COLLATE utf8mb4_bin DEFAULT NULL COMMENT '备注',
  `add_time` datetime NOT NULL COMMENT '创建时间',
  `update_time` datetime DEFAULT NULL COMMENT '更新时间',
  `deleted` tinyint(1) NOT NULL DEFAULT '0' COMMENT '逻辑删除',
  PRIMARY KEY (`id`) USING BTREE
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_bin;
```

#### 1.6 自定义信息表(BEEN_USER_SPECIAL)
| column | type | name | is_null | default | remark |
| :--- | :---: | :---: | :---: | :---: | ---: |
| id | int(11) | 主键 | not null | - | 主键 |
| user_id | int(11) | 所属用户 | not null | - | - |
| name | varchar(255) | 名称 | not null | - | - |
| brief_info | varchar(255) | 简介 | - | - | - |
| detail_info | text | 详情 | - | - | - |
| audit_status | int(1) | 审核状态 | not null | 0 | 0-待审, 1-通过, 2-拒绝 |
| visit_status | int(1) | 访问状态 | not null | 0 | 0-私密, 1-公开 |
| admin_pass | int(11) | 同意人 | - | - | - |
| admin_reject | int(11) | 拒绝人 | - | - | - |
| remark | varchar(63) | 备注 | - | - | - |
| add_time | datetime | 创建时间 | not null | - | - |
| update_time | datetime | 更新时间 | - | - | - |
| deleted | tinyint(1) | 逻辑删除 | not null | 0 | 0-正常, 1-已删除 |

```
CREATE TABLE `been_user_special` (
  `id` int(11) NOT NULL COMMENT '主键',
  `name` varchar(255) COLLATE utf8mb4_bin NOT NULL COMMENT '名称',
  `brief_info` varchar(255) COLLATE utf8mb4_bin NOT NULL COMMENT '简介',
  `detail_info` text COLLATE utf8mb4_bin NOT NULL COMMENT '详情',
  `audit_status` int(1) NOT NULL DEFAULT '0' COMMENT '审核状态, 0-待审核, 1-审核通过, 2-审核拒绝',
  `admin_pass` int(1) DEFAULT NULL COMMENT '同意人',
  `admin_reject` int(1) DEFAULT NULL COMMENT '拒绝人',
  `remark` varchar(255) COLLATE utf8mb4_bin DEFAULT NULL COMMENT '备注',
  `add_time` datetime NOT NULL COMMENT '创建时间',
  `update_time` datetime DEFAULT NULL COMMENT '更新时间',
  `deleted` tinyint(1) NOT NULL DEFAULT '0' COMMENT '逻辑删除',
  PRIMARY KEY (`id`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_bin;
```

#### 1.7 家谱表（BEEN_PEDIGREE）
| column | type | name | is_null | default | remark |
| :--- | :---: | :---: | :---: | :---: | ---: |
| id | int(11) | 主键 | not null | - | 主键 |
| user_id | int(11) | 所属用户 | - | - | - |
| name | varchar(255) | 姓名 | not null | - | - |
| gender | int(1) | 性别 | not null | 0 | 0-未知， 1-男， 2-女 |
| logo_url | varchar(255) | 头像 | not null | - | - |
| brief_info | varchar(255) | 简介 | - | - | - |
| audit_status | int(1) | 审核状态 | not null | 0 | 0-待审, 1-通过, 2-拒绝 |
| spouse_id | int(11) | 配偶 | - | - | - |
| admin_pass | int(11) | 同意人 | - | - | - |
| admin_reject | int(11) | 拒绝人 | - | - | - |
| remark | varchar(63) | 备注 | - | - | - |
| add_time | datetime | 创建时间 | not null | - | - |
| update_time | datetime | 更新时间 | - | - | - |
| deleted | tinyint(1) | 逻辑删除 | not null | 0 | 0-正常, 1-已删除 |
```
CREATE TABLE `been_pedigree` (
  `id` int(11) NOT NULL AUTO_INCREMENT,
  `user_id` int(11) DEFAULT NULL COMMENT '用户',
  `name` varchar(255) COLLATE utf8mb4_bin NOT NULL COMMENT '名称',
  `gender` int(1) NOT NULL COMMENT '性别, 0-未知, 1-男, 2-女',
  `logo_url` varchar(255) COLLATE utf8mb4_bin NOT NULL COMMENT '头像',
  `brief_info` varchar(255) COLLATE utf8mb4_bin DEFAULT NULL COMMENT '简介',
  `audit_status` int(1) NOT NULL DEFAULT '0' COMMENT '审核状态, 0-待审核, 1-审核通过, 2-审核拒绝',
  `spouse_id` int(11) DEFAULT NULL COMMENT '配偶',
  `upper_node` varchar(255) COLLATE utf8mb4_bin NOT NULL DEFAULT '[]' COMMENT '上一辈',
  `lower_node` varchar(255) COLLATE utf8mb4_bin NOT NULL DEFAULT '[]' COMMENT '下一辈',
  `admin_pass` int(1) DEFAULT NULL COMMENT '同意人',
  `admin_reject` int(1) DEFAULT NULL COMMENT '拒绝人',
  `remark` varchar(255) COLLATE utf8mb4_bin DEFAULT NULL COMMENT '备注',
  `add_time` datetime NOT NULL COMMENT '创建时间',
  `update_time` datetime DEFAULT NULL COMMENT '更新时间',
  `deleted` tinyint(1) NOT NULL DEFAULT '0' COMMENT '逻辑删除',
  PRIMARY KEY (`id`) USING BTREE
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_bin;
```

