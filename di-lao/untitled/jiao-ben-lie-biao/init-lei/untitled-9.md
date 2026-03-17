---
description: 地牢复活设置
---

# Revive-Setting

## 脚本参数

标注 **\*** 为必填参数，带有 **\*N** 为支持 英文逗号隔开多个

| 参数              | 说明                                     |
| --------------- | -------------------------------------- |
| revive **\***   | 是否可复活 **(true/false)** #false时死亡直接退出地牢 |
| number \*       | 复活次数                                   |
| death-location  | 是否在死亡点复活 ( **false** 时将在出生点(存档点)位置复活)  |

## 脚本类型

**all** 代表所有的脚本类型都支持

| 类型   | 说明      |
| ---- | ------- |
| init | 地牢启动时执行 |

## 示例

```yaml
$revive-setting{revive=true;number=3;time=10;death-location=true} @init
```
