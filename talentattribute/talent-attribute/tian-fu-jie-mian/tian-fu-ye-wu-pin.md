---
description: 额外扩展配置模块
---

# 天赋页物品

## 作用

配置好的天赋页物品可以通过 **占位符** 快速生成天赋页布局，天赋页物品可以设置 NEXT、LAST、TALENT 三种类型的触发方法，分别为 **下一页、上一页、天赋项** 下面会详细介绍

## 物品方法

| 类型     | 说明                   |
| ------ | -------------------- |
| NEXT   | 点击后会翻至下一页            |
| LAST   | 点击或会翻至上一页            |
| TALENT | 点击后会执行天赋相关的操作(升级、洗点) |

## 配置

物品类型请前往 [GitHub ](https://github.com/TabooLib/taboolib/blob/master/platform/platform-bukkit/src/main/java/taboolib/library/xseries/XMaterial.java)页面查看

{% embed url="https://github.com/TabooLib/taboolib/blob/master/platform/platform-bukkit/src/main/java/taboolib/library/xseries/XMaterial.java" %}

```yaml
#天赋界面布局物品可调用的物品
materials:
  #占位符
  N:
    #物品名
    - name: "&3下一页"
      #方法类型 NEXT / LAST / TALENT
      method: "next"
      #物品类型
      #https://github.com/TabooLib/taboolib/blob/master/platform/platform-bukkit/src/main/java/taboolib/library/xseries/XMaterial.java
      type: "PAPER"
      auto-update: true
      #物品介绍
      info:
        - "&f点击下一页"
        - "&f当前剩余 &c%talent_point_天赋点% &f点天赋点"
  L:
    - name: "&3上一页"
      method: "last"
      type: "PAPER"
      auto-update: true
      info:
        - "&f点击上一页"
        - "&f当前剩余 &c%talent_point_天赋点% &f点天赋点"
  P:
    - name: "&6力量天赋"
      type: "BLUE_STAINED_GLASS_PANE"
      method: "talent"
      #当 method 为 TALENT 时需要将对应天赋KEY填入以下配置项(否则无效)
      talent: "力量天赋"
      #当 method 为 TALENT 时可使用 {talent-level} / {talent-attribute} 占位符
      #读取玩家对应的天赋数据,同时可以使用对应天赋KEY配置内的 formula 数据
      info:
        - "&f当前天赋等级: &c{talent-level}"
        - " "
        - "&f造成伤害就额外增加 &c{0} - {1}"
        - "&f点伤害并,永久增加自身 &c{2} &f点"
        - "&f物理防御"
        - " "
        - "&6SHIFT+右键 &f洗点返还 &c{5} &f点天赋点"
  B:
    - name: "&6嗜血天赋"
      type: "RED_STAINED_GLASS_PANE"
      method: "talent"
      talent: "嗜血天赋"
      info:
        - "&f当前天赋等级: &c{talent-level}"
        - " "
        - "&f当前将有 &c{0}% &f几率触发嗜血技能"
        - "&f对目标造成 &c{1}% &f点伤害并转换为"
        - "&f自身&a生命力"
```
