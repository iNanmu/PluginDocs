---
description: 需安装 HolographicDisplays 全息插件
---

# Hologram 脚本

## 脚本参数

标注 **\*** 为必填参数，带有 **\*N** 为支持 英文逗号隔开多个

| 参数           | 说明                                   |
| ------------ | ------------------------------------ |
| name **\***  | 全息配置名                                |
| operation \* | create(生成) / delete(删除) / update(更新) |
| location     | 生成位置\[X,Y,Z]                         |

## 脚本类型

**all** 代表所有的脚本类型都支持

| 类型      | 说明                                  |
| ------- | ----------------------------------- |
| dungeon | 数据来源地牢系统 (不支持 PlaceholderAPI 变量)    |
| self    | 数据来源地牢系统、触发者 (支持 PlaceholderAPI 变量) |

## 示例

```yaml
$hologram{name=example;operation=create;location=X,Y,Z} @dungeon
```

