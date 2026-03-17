# 装备宝石

## 说明

顾名思义，即往装备上镶嵌不同类型的宝石，提供 **属性** 亦或者 **技能** 效果

你可以在 [扩展示例](./) 这一页中获取到相关的 MythicMobs 物品、技能配置

相比市面上的传统宝石镶嵌插件，我相信 **ItemExtension** 能更加符合你的要求

## 扩展道具配置

该配置插件会默认生成至插件文件夹，你可以不需要复制

```yaml
#道具名
name: "力量宝石"

#全局设置
global:
  #扩展位标识符,不过滤颜色代码
  #即在装备上写 方形 两个字即可被识别为扩展位
  identify: "方形"
  #扩展数量限制,默认为 -1 无限制
  #即一件装备仅允许使用几个该道具
  number: 3
  #扩展道具
  #即通过 ie give 命令获取的物品
  display:
    material: DIAMOND
    name: "§6力量宝石 §fLv.{level}"
    lore:
      - " §f扩展位置: §6方§6形"

levels:
  1:
    #扩展后显示在装备上的内容
    show: "§6力量I"
    #扩展道具属性
    attribute:
      - "物理伤害: 20-50"
    ##放置条件设置
    #condition:
    #  - ...
    #放置触发动作
    wear-action:
      - send inline '§f镶嵌 {{ ie-props name }} §f宝石'
    #拆除触发动作
    tear-action:
      - send inline '§f拆除 {{ ie-props name }} §f宝石'
    #通过 ie give 命令获取该等级道具时额外描述
    info:
      - " "
      - " §e◆ 宝石属性"
      - "   §f物理伤害 +20-50"
  2:
    show: "§6力量II"
    #放置数量限制,默认为 -1 无限制
    #这里的限制优先级大于 全局设置 的限制
    number: 1
    #扩展道具技能
    #需要在 extension-skill 文件夹内配置对应技能
    skill:
      - 力量释放
    attribute:
      - "物理伤害: 30-50"
    wear-action:
      - send inline '§f镶嵌 {{ ie-props name }} §f宝石'
      #修改物品物品名
      - ie name array [ inline "§f充满力量的 {{ ie-item name }}" ]
      #修改物品材质为钻石剑
      - ie itype array [ "DIAMOND_SWORD" ]
      #新增NBT标签数据
      - ie nbt array [ inline "props.{{ ie-props id }}={{ ie-props level }}" ]
    tear-action:
      - send inline '§f拆除 {{ ie-props name }} §f宝石'
      #恢复物品原始名
      - ie del-name array [ true ]
      #恢复物品原始类型
      - ie del-itype array [ true ]
      #删除每个节点的NBT标签数据
      - ie del-nbt array [ inline "props.{{ ie-props id }}" ]
    info:
      - " "
      - " §e◆ 宝石属性"
      - "   §f物理伤害 +50-100"
      - " "
      - " §e◆ 宝石特技"
      - "   §6力量释放 §7(CD:300S)"
      - "   §f攻击时 10% 触发,提高 10% 伤害提升 30S"

#套装效果
#计数: 玩家全身装备上所安装的该扩展道具的数量
suits:
  #数量
  2:
    #套装属性
    attribute:
      - "物理伤害: 100"
  #数量
  3:
    #套装属性
    attribute:
      - "物理伤害: 200"
    #套装技能
    #skill:
    #  - "技能名"
```

## 扩展技能配置

```yaml
#技能名
力量释放:
  #触发类型
  type: "ATTACK"
  #是否唯一效果,默认为是
  #即多个装备拥有该技能的扩展道具时只触发一次
  only: true
  #冷却时间
  #当为 RUNTIME 触发类型时,该项为循环间隔时间
  cooling: 300
  #触发条件
  action-conditions:
    - check random 100.0 >= 50.0
  #触发效果
  actions:
    - send '§6力量释放! §f提高物理伤害 10% 持续 30S'
    - command 'ap persistent %player_name% 力量释放宝石效果 物理伤害:10(%) 30'

#技能名
生命恢复:
  type: "RUNTIME"
  only: true
  #当为 RUNTIME 触发类型时,该项为循环间隔时间
  cooling: 300
  actions:
    - send '§6生命恢复! §f获得 200 生命恢复效果,持续 10S'
    - command 'ap persistent %player_name% 生命恢复宝石效果 生命恢复:200 30'
```

## 扩展界面配置

```yaml
#界面名
name: "宝石镶嵌"
#界面标题
title: "宝石镶嵌"

#界面布局
layout:
  #页数
  1:
    - "####I####"
    - "# ■ ■ ■ #"
    - "∧#######∨"
  2:
    - "####I####"
    - "# ◆ ◆ ◆ #"
    - "∧#######∨"

#下方配置内的 I ∧ ∨ 固定为物品位、上一页、下一页按键
material:
  "■":
    material: BARRIER
    name: "§f宝石扩展位"
    lore:
      - "§f请放入 §6方形 §f类型扩展宝石"
    #允许放入的扩展位识别符
    #即扩展道具配置内的 identify 配置
    identify: "方形"
  "◆":
    material: BARRIER
    name: "§f宝石扩展位"
    lore:
      - "§f请放入 §3菱形 §f类型扩展宝石"
    identify: "菱形"
  "I":
    material: BARRIER
    name: "§f装备位"
    lore:
      - "§f请放入需要扩展的装备"
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
