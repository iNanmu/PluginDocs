---
description: 从 1.1.4 版本起支持该功能
---

# 区域限制

## 脚本区域限制说明

该功能可以限制某一行脚本执行 **只对某个** [**地牢区域**](../di-lao-qu-yu.md) **内的玩家触发** 效果，在区域外的玩家不触发效果，该功能需要提前在地牢配置中的 **OPTIONE.YML** 配置内设置 **DUNGEON-AREA** 地牢区域，需要注意的是不管你配置里面脚本行触发类型设置的是 **@DUNGEON** 还是 **@PLAYER** 只要使用了 **区域触发格式的脚本行** 那触发类型就一定是 **@SELF** 所以只能在 **SELF** 类型的 **脚本、占位符** 上使用该功能

## 特别说明

当区域名设为 **\~@ALL** 时，将以整个地牢内玩家为触发者并以 **SELF** 运行类型触发脚本

## 使用时的脚本格式

$command{text=say \<self:player-name> 在 \<self:area-name> 区域内} @player **\~区域名,...**

{% hint style="info" %}
区域名支持多个，可用 "," 符号分隔，例如 **\~区域一,区域二** 注意这个脚本区域限制是可加可不加的，看自己需求
{% endhint %}

## 例子

假设 **怪物组A** 位于 **区域A** 的地牢区域内

```yaml
groups:
  怪物组A:
  - monster:
    - $mob{plugin=MythicMobs;name=狂暴村民;location=1804.0,3.0,964.0;amount=4;scattered=1} @dungeon
    condition:
    - $kill{mobname=狂暴村民;amount=4} @system
    start:
    - $message{type=text;text=狂暴村民出现了!} @dungeon
    end:
    #给在 区域A 内的玩家发送消息
    - $message{text=say <self:player-name> 你成功清除 <self:area-name> 区域怪物} @self ~区域A
    #给在 区域A 内的玩家发送奖励
    - $command{text=exp give <self:player-name> 1000} @self ~区域A
    #给在地牢内的所有玩家发送一条消息
    - $message{type=text;text=区域A怪物已被清除} @dungeon
```

