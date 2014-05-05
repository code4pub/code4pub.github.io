---
layout: post
title: "Mybatis Migrations Maven插件常用命令"
description: "MyBatis的数据库迁移插件，可以使用配置管理的思想方便的管理数据库"
category: tech
tags: [MyBatis]
---
{% include JB/setup %}

##MyBatis数据库迁移MVN插件
官方文档地址：[MyBatis Migrations Maven plugin](http://mybatis.github.io/migrations-maven-plugin/){:target="_blank"}
###命令介绍
格式：`mvn migration:命令`
- `status`:检查当前所有SQL脚本的状态，如果执行过了，则在"Applied At"中会显是执行的时间
- `new`: 创建新的SQL脚本。如: mvn migration:new -Dmigration.description="create user table"
- `up`:  执行所有未执行的SQL脚本
- `down`: 执行上一条执行过的SQL脚本中的`@UNDO`部分

- `check`：检查所有`未执行`（pending）的SQL脚本
- `pending`：执行所有`未执行`的SQL脚本
- `version`：执行某一SQL脚本，该脚本的`版本(version)`为`ID`值，通常为创建的时间。
- `script`：执行特定的SQL脚本。

- `init`：创建MyBatis一份新的迁移仓库（目录）。如果已经创建好了相关目录，则不需要执行。通常仅需执行一次。
- `bootstrap`：执行`bootstrap.sql`里的内容。通常是在本机第一次执行SQL命令来初始化数据库时用。

##Tips
- 执行new之后，需要检查生成的SQL文件的编码格式是否是UTF-8。
- 先写`@UNDO`部分。方便up时出错。
