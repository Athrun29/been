# DB-USER

## 数据库设计

### 1. 系统基础

#### 1.1 用户表(BEEN_USER)
| column | type | name | is_null | default | remark |
| :--- | :---: | :---: | :---: | :---: | ---: |
| id | int(11) | 主键 | not null | - | 主键 |
| name | varchar(255) | 姓名 | not null | - | - |
| code | varchar(32) | 编号 | not null | - | - |
| username | varchar(255) | 账号 | not null | - | - |
| password | varchar(255) | 密码 | not null | - | - |
| auth_pwd | varchar(255) | 访问密码 | - | - | - |
| trust_admin | int(11) | 委托管理员 | - | - | - |
| trust_user | int(11) | 委托用户 | - | - | - |
| role_type | int(1) | 角色类型 | not null | 0 | 0-未知, 1-超管, 2-编辑, 3-审核, 4-普通 |
| nickname | varchar(255) | 昵称 | not null | '' | - |
| avatar | varchar(255) | 头像 | - | '' | - |
| logo_url | varchar(255) | 肖像 | - | '' | - |
| back_url | varchar(255) | 背景 | - | '' | - |
| qr_code | blob | 二维码 | - | - | - |
| mobile | varchar(255) | 手机号 | - | - | - |
| id_card | varchar(255) | 身份证 | - | - | - |
| mail | varchar(255) | 邮箱 | - | - | - |
| gender | int(1) | 性别 | not null | 0 | 0-未知， 1-男， 2-女 |
| birthday | date | 生日 | - | - | - |
| weixin_openid | varchar(63) | 微信服务号openid | not null | - | - |
| mini_openid | varchar(63) | 微信小程序openid | not null | - | - |
| remark | varchar(63) | 备注 | - | - | - |
| last_login_time | datetime | 最后登陆时间 | - | - | - |
| last_login_ip | int(11) | 最后登陆ip | - | - | - |
| status | int(1) | 状态 | not null | - | 0 可用, 1 禁用, 2 注销 |
| add_time | datetime | 创建时间 | not null | - | - |
| update_time | datetime | 更新时间 | - | - | - |
| deleted | tinyint(1) | 逻辑删除 | not null | 0 | 0-正常, 1-已删除 |

```
CREATE TABLE `been_user` (
  `id` int(11) NOT NULL AUTO_INCREMENT,
  `username` varchar(255) COLLATE utf8mb4_bin NOT NULL,
  `password` varchar(255) COLLATE utf8mb4_bin NOT NULL,
  `name` varchar(255) COLLATE utf8mb4_bin NOT NULL DEFAULT '' COMMENT '姓名',
  `code` varchar(255) COLLATE utf8mb4_bin NOT NULL COMMENT '编号',
  `logo_url` varchar(255) COLLATE utf8mb4_bin DEFAULT NULL COMMENT '照片',
  `back_url` varchar(255) COLLATE utf8mb4_bin DEFAULT NULL COMMENT '背景',
  `auth_pwd` varchar(255) COLLATE utf8mb4_bin DEFAULT NULL COMMENT '模块密码',
  `trust_admin` int(11) DEFAULT NULL COMMENT '托管的管理员',
  `trust_user` int(11) DEFAULT NULL COMMENT '托管的用户',
  `role_type` int(1) NOT NULL DEFAULT '0' COMMENT '角色类型, 0-未知, 1-超管, 2-编辑, 3-审核, 4-普通',
  `nickname` varchar(255) COLLATE utf8mb4_bin DEFAULT '' COMMENT '昵称',
  `avatar` varchar(255) CHARACTER SET utf8mb4 DEFAULT '' COMMENT '用户头像图片',
  `qr_code` blob COMMENT '二维码',
  `mobile` varchar(255) COLLATE utf8mb4_bin NOT NULL COMMENT '手机号',
  `id_card` varchar(32) COLLATE utf8mb4_bin DEFAULT NULL COMMENT '身份证',
  `mail` varchar(255) COLLATE utf8mb4_bin DEFAULT NULL COMMENT '邮箱',
  `gender` int(1) NOT NULL DEFAULT '0' COMMENT '性别：0 未知， 1男， 2 女',
  `birthday` date DEFAULT NULL COMMENT '生日',
  `weixin_openid` varchar(63) CHARACTER SET utf8mb4 NOT NULL DEFAULT '' COMMENT '微信登录openid',
  `mini_openid` varchar(63) CHARACTER SET utf8mb4 NOT NULL DEFAULT '' COMMENT '小程序openid',
  `remark` varchar(255) CHARACTER SET utf8mb4 DEFAULT NULL COMMENT '备注',
  `last_login_time` datetime DEFAULT NULL COMMENT '最近一次登录时间',
  `last_login_ip` varchar(63) CHARACTER SET utf8mb4 DEFAULT '' COMMENT '最近一次登录IP地址',
  `status` int(1) NOT NULL DEFAULT '0' COMMENT '0 可用, 1 禁用, 2 注销',
  `add_time` datetime NOT NULL COMMENT '创建时间',
  `update_time` datetime DEFAULT NULL COMMENT '更新时间',
  `deleted` tinyint(1) NOT NULL DEFAULT '0' COMMENT '逻辑删除',
  PRIMARY KEY (`id`) USING BTREE
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_bin;
```

#### 1.2 权限表(BEEN_PERM)
| column | type | name | is_null | default | remark |
| :--- | :---: | :---: | :---: | :---: | ---: |
| id | int(11) | 主键 | not null | - | 主键 |
| name | varchar(127) | 名称 | not null | - | - |
| perm_url | varchar(127) | 权限url | not null | - | - |
| menu_status | int(1) | 菜单标识 | not null | - | 0-否, 1-是 |
| anon_status | int(1) | 匿名标识 | not null | - | 0-否, 1-是 |
| remark | varchar(255) | 备注 | - | - | - |
| add_time | datetime | 创建时间 | not null | - | - |
| update_time | datetime | 更新时间 | - | - | - |
| deleted | tinyint(1) | 逻辑删除 | not null | 0 | 0-正常, 1-已删除 |

```
CREATE TABLE `been_perm` (
  `id` int(11) NOT NULL AUTO_INCREMENT,
  `name` varchar(127) COLLATE utf8mb4_bin NOT NULL COMMENT '名称',
  `perm_url` varchar(127) COLLATE utf8mb4_bin NOT NULL COMMENT 'url',
  `menu_status` int(1) NOT NULL DEFAULT '0' COMMENT '是否菜单, 0-否, 1-是',
  `anon_status` int(1) NOT NULL DEFAULT '0' COMMENT '是否开放, 0-否, 1-是',
  `remark` varchar(255) COLLATE utf8mb4_bin DEFAULT NULL COMMENT '备注',
  `add_time` datetime NOT NULL COMMENT '创建时间',
  `update_time` datetime DEFAULT NULL COMMENT '更新时间',
  `deleted` tinyint(1) NOT NULL DEFAULT '0' COMMENT '逻辑删除',
  PRIMARY KEY (`id`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_bin;
```

#### 1.3 角色表(BEEN_ROLE)
| column | type | name | is_null | default | remark |
| :--- | :---: | :---: | :---: | :---: | ---: |
| id | int(11) | 主键 | not null | - | 主键 |
| name | varchar(127) | 名称 | not null | - | - |
| sys_name | varchar(127) | 系统简称(英文) | not null | - | - |
| remark | varchar(255) | 备注 | - | - | - |
| add_time | datetime | 创建时间 | not null | - | - |
| update_time | datetime | 更新时间 | - | - | - |
| deleted | tinyint(1) | 逻辑删除 | not null | 0 | 0-正常, 1-已删除 |

```
CREATE TABLE `been_role` (
  `id` int(11) NOT NULL,
  `name` varchar(127) COLLATE utf8mb4_bin NOT NULL COMMENT '名称',
  `sys_name` varchar(127) COLLATE utf8mb4_bin NOT NULL COMMENT '系统简称(英文)',
  `remark` varchar(255) COLLATE utf8mb4_bin DEFAULT NULL COMMENT '备注',
  `add_time` datetime NOT NULL COMMENT '创建时间',
  `update_time` datetime DEFAULT NULL COMMENT '更新时间',
  `deleted` tinyint(1) NOT NULL DEFAULT '0' COMMENT '逻辑删除',
  PRIMARY KEY (`id`) USING BTREE
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_bin;
```

#### 1.4 角色-权限表(BEEN_ROLE_PERM)
| column | type | name | is_null | default | remark |
| :--- | :---: | :---: | :---: | :---: | ---: |
| id | int(11) | 主键 | not null | - | 主键 |
| role_id | int(11) | 角色id | not null | - | - |
| perm_id | int(11) | 权限id | not null | - | - |
| add_time | datetime | 创建时间 | not null | - | - |
| update_time | datetime | 更新时间 | - | - | - |
| deleted | tinyint(1) | 逻辑删除 | not null | 0 | 0-正常, 1-已删除 |

```
CREATE TABLE `been_role_perm` (
  `id` int(11) NOT NULL AUTO_INCREMENT,
  `role_id` int(11) NOT NULL COMMENT '角色',
  `perm_id` int(11) NOT NULL COMMENT '权限',
  `add_time` datetime NOT NULL COMMENT '创建时间',
  `update_time` datetime DEFAULT NULL COMMENT '更新时间',
  `deleted` tinyint(1) NOT NULL DEFAULT '0' COMMENT '逻辑删除',
  PRIMARY KEY (`id`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_bin;
```

#### 1.5 用户-角色表(BEEN_USER_ROLE)
| column | type | name | is_null | default | remark |
| :--- | :---: | :---: | :---: | :---: | ---: |
| id | int(11) | 主键 | not null | - | 主键 |
| user_id | int(11) | 用户id | not null | - | - |
| role_id | int(11) | 角色id | not null | - | - |
| add_time | datetime | 创建时间 | not null | - | - |
| update_time | datetime | 更新时间 | - | - | - |
| deleted | tinyint(1) | 逻辑删除 | not null | 0 | 0-正常, 1-已删除 |

```
CREATE TABLE `been_user` (
  `id` int(11) NOT NULL AUTO_INCREMENT,
  `username` varchar(255) COLLATE utf8mb4_bin NOT NULL,
  `password` varchar(255) COLLATE utf8mb4_bin NOT NULL,
  `name` varchar(255) COLLATE utf8mb4_bin NOT NULL DEFAULT '' COMMENT '姓名',
  `code` varchar(32) COLLATE utf8mb4_bin NOT NULL COMMENT '用户编号',
  `logo_url` varchar(255) COLLATE utf8mb4_bin DEFAULT NULL COMMENT '照片',
  `back_url` varchar(255) COLLATE utf8mb4_bin DEFAULT NULL COMMENT '背景',
  `auth_pwd` varchar(255) COLLATE utf8mb4_bin DEFAULT NULL COMMENT '模块密码',
  `trust_admin` int(11) DEFAULT NULL COMMENT '委托内容管理员',
  `trust_user` int(11) DEFAULT NULL COMMENT '托管的帐号',
  `role_type` int(11) NOT NULL DEFAULT '0' COMMENT '角色类型, 0-未知, 1-超管, 2-编辑, 3-审核, 4-普通',
  `nickname` varchar(255) COLLATE utf8mb4_bin DEFAULT '' COMMENT '昵称',
  `avatar` varchar(255) CHARACTER SET utf8mb4 DEFAULT '' COMMENT '用户头像图片',
  `qr_code` blob COMMENT '二维码',
  `mobile` varchar(255) COLLATE utf8mb4_bin NOT NULL COMMENT '手机号',
  `id_card` varchar(32) COLLATE utf8mb4_bin DEFAULT NULL COMMENT '身份证',
  `mail` varchar(255) COLLATE utf8mb4_bin DEFAULT NULL COMMENT '邮箱',
  `gender` int(1) NOT NULL DEFAULT '0' COMMENT '性别：0 未知， 1男， 2 女',
  `birthday` date DEFAULT NULL COMMENT '生日',
  `weixin_openid` varchar(63) CHARACTER SET utf8mb4 NOT NULL DEFAULT '' COMMENT '微信登录openid',
  `mini_openid` varchar(63) CHARACTER SET utf8mb4 NOT NULL DEFAULT '' COMMENT '小程序openid',
  `remark` varchar(255) CHARACTER SET utf8mb4 DEFAULT NULL COMMENT '备注',
  `last_login_time` datetime DEFAULT NULL COMMENT '最近一次登录时间',
  `last_login_ip` varchar(63) CHARACTER SET utf8mb4 DEFAULT '' COMMENT '最近一次登录IP地址',
  `status` int(1) NOT NULL DEFAULT '0' COMMENT '0 可用, 1 禁用, 2 注销',
  `add_time` datetime NOT NULL COMMENT '创建时间',
  `update_time` datetime DEFAULT NULL COMMENT '更新时间',
  `deleted` tinyint(1) NOT NULL DEFAULT '0' COMMENT '逻辑删除',
  PRIMARY KEY (`id`) USING BTREE
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_bin;
```
