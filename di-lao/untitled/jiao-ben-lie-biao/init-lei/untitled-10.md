---
description: 设置地牢是否允许破坏/放置方块等内容
---

# Setting

## 脚本参数

标注 **\*** 为必填参数，带有 **\*N** 为支持 英文逗号隔开多个

| 参数                     | 说明                    |
| ---------------------- | --------------------- |
| break                  | 是否可破坏方块 (true/false)  |
| place                  | 是否可放置方块 (true/false)  |
| pvp                    | 是否开启队内伤害 (true/false) |
| mode                   | 游戏模式                  |
| rejoin (default:false) | 在副本内重新登陆时固定登陆点为副本重生点  |

## 脚本类型

**all** 代表所有的脚本类型都支持

| 类型   | 说明      |
| ---- | ------- |
| init | 地牢启动时执行 |

## 示例

```yaml
$setting{break=false;place=false;mode=ADVENTURE} @init
```

## 特别说明

这个脚本设置不会影响到地牢交互脚本的运行
