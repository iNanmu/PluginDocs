---
description: 地牢任务(DungeonTask)操作
---

# Task

## 脚本参数

标注 **\*** 为必填参数，带有 **\*N** 为支持 英文逗号隔开多个

| 参数           | 说明                                       |
| ------------ | ---------------------------------------- |
| name **\***  | 任务名                                      |
| operation \* | 操作 **start(启动) / end(结束) / restart(重启)** |
| mode \*      | 模式 **timing(定时) / cycle(循环)**            |
| async \*     | 是否异步执行 **(true/false)**                  |

## 脚本类型

**all** 代表所有的脚本类型都支持

| 类型      | 说明    |
| ------- | ----- |
| dungeon | 由地牢执行 |

## 示例

```yaml
$task{name=任务名;operation=start;mode=timing;async=true} @dungeon
```
