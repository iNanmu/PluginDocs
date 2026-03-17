---
description: 触发怪物组 (需要安装 MythicMobs 插件)
---

# MonsterGroup

## 脚本参数

标注 **\*** 为必填参数，带有 **\*N** 为支持 英文逗号隔开多个

| 参数           | 说明                              |
| ------------ | ------------------------------- |
| group **\*** | 怪物组名称 **\*N**                   |
| repeat \*    | 单局地牢游戏是否可以触发多次 **(true/false)** |
| delay        | 延迟触发                            |

## 脚本类型

**all** 代表所有的脚本类型都支持

| 类型      | 说明    |
| ------- | ----- |
| dungeon | 由地牢执行 |

## 示例

```yaml
$monstergroup{group=default;repeat=false;delay=1} @dungeon
```
