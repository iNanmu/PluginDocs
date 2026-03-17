---
description: 执行命令
---

# Command

## 脚本参数

标注 **\*** 为必填参数，带有 **\*N** 为支持 英文逗号隔开多个

| 参数           | 说明                                |
| ------------ | --------------------------------- |
| text **\***  | 命令 **\*N**                        |
| console      | 是否以后台执行 (true/false) 默认 **false** |
| death-player | 是否奖励已死亡的队员,默认 **false**           |
| chance       | 概率触发                              |

## 脚本类型

**all** 代表所有的脚本类型都支持

| 类型      | 说明              |
| ------- | --------------- |
| dungeon | 由服务器后台执行一次命令    |
| player  | 由地牢内的所有玩家执行一次命令 |
| self    | 由触发者执行一次命令      |

## 示例

```yaml
$command{text=fly <player.name>,say %player_name% 触发飞行模式;console=false;death-player=false} @player
```
