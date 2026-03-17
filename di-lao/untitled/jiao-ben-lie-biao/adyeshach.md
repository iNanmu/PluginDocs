---
description: 召唤 Adyeshach/Citizens 插件 NPC
---

# Npc

## 脚本参数

标注 **\*** 为必填参数，带有 **\*N** 为支持 英文逗号隔开多个

| 参数           | 说明                                     |
| ------------ | -------------------------------------- |
| type \*      | NPC插件 **A**(Adyeshach) **C**(Citizens) |
| id **\***    | NPC-ID                                 |
| operation \* | spawn(生成)/delete(删除)                   |
| location     | 生成位置\[X,Y,Z]                           |

## 脚本类型

**all** 代表所有的脚本类型都支持

| 类型      | 说明    |
| ------- | ----- |
| dungeon | 由地牢执行 |

## 示例

```yaml
$anpc{type=a;id=test;operation=spawn;location=X,Y,Z} @dungeon
```
