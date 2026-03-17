---
description: DungeonInteract
---

# 地牢交互

## 地牢交互脚本

地牢交互脚本是基于 **ActionScript** 而开发的功能，所有的处理都依靠 **ActionScript** 脚本\
它可以让你在地牢内设置不同类型的交互脚本，这是 **ActionScript** 无法单独完成的功能

## 地牢交互类型

每个交互类型所需设置的参数各有不同，具体还是由 **交互类型的开发者** 所定，插件 **原生** 的交互类型具体可以看下一页文档的内容

什么由交互类型的开发者所定？也就是说可以自定义交互类型？\
**当然**，由于 **DungeonPlus开发者** 无法将所有的交互类型都写出来，只写了点基础的类型，有需要的可以查看 [**API (BasicInteractScript)**](https://ersha.gitbook.io/dungeonplus/kai-fa-zhe/undefined) 它可以帮助你注册一个全新的交互脚本类型

## 地牢交互脚本要怎么启动

与 DungeonTask 相同，为了能够更加灵活操作地牢内的流程，交互脚本也需要通过 ActionScript 脚本来启动或结束，脚本为 **$interact** 例如 **"$interact{type=脚本类型;name=交互脚本名;operation=start} @dungeon"** 来执行启动操作，你也可以通过配置上的 **auto-start** 项目做到地牢启动时自启交互组

## 配置格式

```yaml
#交互类型 (需要大写)
type: PLAYER_DEATH
#交互参数 (注意需要使用 "" 包括参数值)
parameter:
  level: "100"
  permission: "none"

#是否仅触发一次
first: false
#地牢启动时自启,默认关闭
#关闭后想要通过 Interact 交互脚本进行启动
auto-start: false
#交互后执行脚本内容
script:
  - $message{type=text;text=<self:player-name> 死翘翘了} @self
```
