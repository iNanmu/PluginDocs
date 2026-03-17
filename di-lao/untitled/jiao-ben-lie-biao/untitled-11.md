---
description: 地牢交互脚本(DungeonInteract)操作
---

# Interact

## 脚本参数

标注 **\*** 为必填参数，带有 **\*N** 为支持 英文逗号隔开多个

| 参数           | 说明                              |
| ------------ | ------------------------------- |
| type **\***  | 交互类型                            |
| name \*      | 交互脚本名 **( interact 文件夹内对应名字 )** |
| operation \* | 操作 **start(启动) / end(结束)**      |

## 脚本类型

**all** 代表所有的脚本类型都支持

| 类型      | 说明    |
| ------- | ----- |
| dungeon | 由地牢执行 |

## 示例

```yaml
$interact{type=交互类型;name=交互脚本名;operation=start} @dungeon
```
