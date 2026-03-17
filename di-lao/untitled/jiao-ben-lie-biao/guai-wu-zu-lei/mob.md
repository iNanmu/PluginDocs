---
description: 在指定区域召唤怪物 (需要安装 MythicMobs 插件)
---

# Mob

## 脚本参数

标注 **\*** 为必填参数，带有 **\*N** 为支持 英文逗号隔开多个

| 参数            | 说明                    |
| ------------- | --------------------- |
| plugin **\*** | 目前仅支持 MythicMobs 怪物插件 |
| name \*       | 怪物名                   |
| location \*   | 生成位置 (X,Y,Z)          |
| amount \*     | 生成数量                  |
| scattered \*  | 生成间隔                  |
| level         | 怪物等级,默认为 **0**        |
| yaw           | 视角朝向                  |
| pitch         | 俯仰角朝向                 |
| chance        | 生成的几率                 |

## 脚本类型

**all** 代表所有的脚本类型都支持

| 类型      | 说明    |
| ------- | ----- |
| dungeon | 由地牢执行 |

## 示例

```yaml
$mob{plugin=MythicMobs;name=怪物;location=x,y,z;amount=1;scattered=1.0} @dungeon
```

## 特别说明

这个脚本手动配置会比较麻烦，可以使用插件的在线编辑功能进行快捷设置，具体查看 **地牢编辑** 章节
