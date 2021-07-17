# bt
blog tool

bt继承自博客工具链bt

文档和bt保持一致

因为bt不开源的原因 bt将作为单独公开分支开发

类似hexo的自动md工具

## 命令行参数

```bash
./bt -h
NAME:
   bt - bt -h

USAGE:
   bt是一个md一键式工具

VERSION:
   1.2 20210316

DESCRIPTION:
   github.com/landers1037/bt

COMMANDS:
   help, h  Shows a list of commands or help for one command
   database:
     db, db, newdb, dbcreate         db -t N [file Path] [db name]
     dbu, dbu, updatedb, dbupdate    dbu [file] [db name]
     dbt, dbt, updatetable, dbtable  dbt [table] [where] [data] [db name]
   md:
     new, n, new, newmd     new example
     test, t, test, testmd  test file.md

GLOBAL OPTIONS:
   --help, -h     show help (default: false)
   --version, -v  print the version (default: false)

COPYRIGHT:
   Landers - renj.io
```

## 文件分组

### 新建

使用new命令可以新建一篇格式化的md文件

new后面的参数即文件名

```bash
./bt new hello_world
```

**hello_world.md**

```markdown
---
title: hello_world
name: hello_world
date: 2021-03-16 01:15:28
id: 0
tags: 
categories: 
abstract: 
---
<!--more-->
```

上面使用`---`分割的为bt需要读取的yaml前置格式化文本，里面的参数解释请参考指导文档

### 定制模板

如果你不想要默认的yaml头部文本样式，你可以自己定义

请注意：如果你定义后规范和bt规范不一致将会导致解析失败

```bash
# 查看当前的模板内容
./bt -s

---
title: %s
name: %s
date: %s
id: 0
tags: 
categories: 
abstract: 
---
<!--more-->

# 修改模板
./bt new -e
```



## 数据库分组

使用db相关的命令来创建数据库或者迁移数据库

### 新建数据库

此命令将帮助你将md文件写入到数据库中以供blog服务读取

```bash
NAME:
   bt db - db -t N [file Path] [db name]

USAGE:
   创建博客数据库

CATEGORY:
   database

OPTIONS:
   -t value, --thread value  -t 10 (default: 10)
   --help, -h                show help (default: false)
```

-t 参数为指定使用的线程数 当文件过多时使用多线程方便更快的解析

`file path` 存放md文件的路径 请确保此路径下仅存在md文件 且符合bt的规范

`db name` 需要生成的数据库名称 默认为blog.db

### 更新数据库

仅为更新某篇文章的数据库内容

```bash
 ./bt dbu test.md blog.db
```

### 高级更新数据库

指定数据库表名 条件 要更新的值即可更新数据

```bash
./bt dbt db_blog_post "name = pin" "id = 1" blog.db
```

