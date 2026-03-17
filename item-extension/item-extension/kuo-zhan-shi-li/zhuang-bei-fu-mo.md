# 装备附魔

## 说明

顾名思义，利用 [扩展语句](../kuo-zhan-yu-ju.md) 为扩展装备附属不同的附魔效果

你可以在 [扩展示例](./) 这一页中获取到相关的 MythicMobs 物品

## 扩展道具配置

该配置插件会默认生成至插件文件夹，你可以不需要复制

```yaml
#道具名
name: "锋利附魔石"

#全局设置
global:
  #扩展位标识符,不过滤颜色代码
  #即在装备上写 附魔 两个字即可被识别为扩展位
  identify: "附魔"

  #设置全局使用数量
  #即一件装备只能装备一个锋利附魔石
  number: 1

  #全局放置动作设置
  #即向装备扩展位放置该配置下的所有道具均会触发
  wear-action:
    - send inline '§f镶嵌 {{ ie-props show }} §f附魔石'
    #新增力量附魔效果,支持数字附魔ID
    #通过 {{ ie-props level }} 占位符获取宝石等级
    - ie enchant array [ inline damage_all {{ ie-props level }} ]

  #全局拆除动作设置
  #即向装备扩展位拆除该配置下的所有道具均会触发
  tear-action:
    - send inline '§f拆除 {{ ie-props show }} §f附魔石'
    #删除物品上的某一附魔,支持数字附魔ID
    - ie del-enchant array [ damage_all ]

  #扩展道具
  display:
    material: DIAMOND
    name: "§5锋利附魔石 §fLv.{level}"
    lore:
      - " §f扩展位置: §6附§6魔"

levels:
  1:
    show: "§b锋利I"
    info:
      - " "
      - " §e◆ 附魔效果"
      - "   §f锋利 I"
  2:
    show: "§b锋利II"
    info:
      - " "
      - " §e◆ 附魔效果"
      - "   §f锋利 II"
```

## 扩展界面配置

```yaml
name: "附魔台"
title: "附魔台"
layout:
  1:
    - "####I####"
    - "# ■ ■ ■ #"
    - "# ■ ■ ■ #"
    - "#########"

#下方配置内的 I ∧ ∨ 固定为物品位、上一页、下一页按键
material:
  "■":
    material: BARRIER
    name: "§f附魔扩展位"
    lore:
      - "§f请放入附魔石"
    identify: "附魔"
  "I":
    material: BARRIER
    name: "§f装备位"
    lore:
      - "§f请放入需要附魔的装备"
  "∧":
    material: PAPER
    name: "§7上一页"
  "∨":
    material: PAPER
    name: "§7下一页"
  "#":
    material: GRAY_STAINED_GLASS_PANE
    name: "§7边框"
```
