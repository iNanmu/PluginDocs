---
description: 地牢数据(DungeonMeta)操作
---

# Data

## 脚本参数

标注 **\*** 为必填参数，带有 **\*N** 为支持 英文逗号隔开多个

| 参数           | 说明                                      |
| ------------ | --------------------------------------- |
| key **\***   | 数据名                                     |
| type \*      | 数据类型 **value(数值) / list(列表)**           |
| operation \* | 数据操作 **add(增加) / take(减少) / reset(重置)** |
| value \*     | 值                                       |

## 脚本类型

**all** 代表所有的脚本类型都支持

| 类型      | 说明    |
| ------- | ----- |
| dungeon | 由地牢执行 |

## 示例

```yaml
$data{key=数据名;type=value;operation=<add/take/reset>;value=值} @dungeon
```
