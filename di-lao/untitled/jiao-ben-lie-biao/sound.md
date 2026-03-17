---
description: 触发游戏音效
---

# Sound

## 脚本参数

标注 **\*** 为必填参数，带有 **\*N** 为支持 英文逗号隔开多个

| 参数          | 说明                                                                   |
| ----------- | -------------------------------------------------------------------- |
| type **\*** | 音效类型 ([列表](https://bukkit.windit.net/javadoc/org/bukkit/Sound.html)) |

## 脚本类型

**all** 代表所有的脚本类型都支持

| 类型             | 说明         |
| -------------- | ---------- |
| dungeon、player | 向地牢内所有玩家发送 |
| self           | 向触发者发送     |

## 示例

```yaml
$sound{type=ENTITY_ENDERDRAGON_FIREBALL_EXPLODE} @dungeon
```
