---
description: 该功能从 1.0.8 版本开始
---

# 启动参数

## 地牢启动参数

这个东西是为了更好的控制地牢难度而不用去重复的复制同一份地牢配置跟地图，地牢启动参数设置方法为 **dp start <地牢> <启动参数>** 这个启动参数是可有可无的，接下来就是在地牢内获取启动参数，获取启动参数需要使用 **\<dungeon:params \*参数位>** 地牢占位符

## 例子

在地牢启动时发送地牢启动参数的内容，并使用 dp start 地牢 **测试参数;DungeonPlus** 命令，后面所设置的**测试参数;DungeonPlus** 就是地牢启动参数

```yaml
dungeon-init-script:
- $setmap{name=test} @init
dungeon-start:
  condition: []
  action-script:
  #这里的地牢占位符将显示 测试参数
  - $message{type=text;text=启动参数内容 '<dungeon:params *1 *默认值>'} @dungeon
  #这里的地牢占位符将显示 DungeonPlus
  - $message{type=text;text=启动参数内容 '<dungeon:params *2 *默认值>'} @dungeon
dungeon-reward-script: []
```
