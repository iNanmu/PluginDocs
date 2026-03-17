# 装备赋能

## 说明

类似某某勇者手游的武器专属技能效果，通过放置足够的扩展道具，激活对应词条效果

示例中搭配 **套装系统、技能系统** 作出了这一效果，技能为 MythicMobs 技能

你可以在 [扩展示例](./) 这一页中获取到相关的 MythicMobs 物品、技能配置

## 扩展道具配置

该配置插件会默认生成至插件文件夹，你可以不需要复制

```yaml
name: "星陨石"

global:
  #装备槽位标识符
  identify: "空缺"
  display:
    material: DIAMOND
    name: "§5§l星陨石"
    lore:
      - "§f可为 §6星陨剑 §f武器增加星陨能量"
      - "§f并同时增加 §6+50 §f点物理伤害"

levels:
  1:
    #安装扩展道具后描述描述替换为以下内容
    show: "§5星陨"
    #扩展道具属性
    attribute:
      - "物理伤害: 50"
    #是否允许拆除(默认允许)
    dismantle: false
    #判断放入的物品是否为 §6星陨剑
    #可以根据这个判断,为不同的武器写不同的扩展道具
    condition:
      - check {{ ie-item name }} == '§6星陨剑'

#套装效果多件装备只生效一个，但多件装备上的宝石件数会合计
#利用该功能，模拟激活词条的效果
suits:
  1:
    attribute:
      - "暴击伤害: 50"
  2:
    attribute:
      - "暴击几率: 10"
  3:
    attribute:
      - "物理伤害: 100"
    skill:
      - 星陨技能
```

## 扩展技能配置

```yaml
#技能名
星陨技能:
  #触发类型
  type: "ATTACK"
  #是否唯一效果,默认为是
  #即多个装备拥有该技能的扩展道具时只触发一次
  only: true
  #冷却时间
  cooling: 10
  #触发条件
  action-conditions:
    #模拟概率
    - check random 100.0 >= 80.0
  actions:
    #使用 MythicMobs 插件技能
    #同时兼容 SkillAPI Planners 插件技能,详细查看 扩展语句 介绍
    - mythic-skill 陨星释放 1.0
    - send '§c§l星陨 §f技能进入 §610 §f秒冷却'
```

## 扩展界面配置

```yaml
name: "装备赋能台"
title: "装备赋能台"
layout:
  1:
    - "####I####"
    - "# ■ ■ ■ #"
    - "#########"

material:
  "■":
    material: BARRIER
    name: "§6能量石"
    lore:
      - "§f请放入对应武器的能量石"
    identify: "空缺"
  "I":
    material: BARRIER
    name: "§f装备位"
    lore:
      - "§f请放入需要扩展的装备"
  "#":
    material: GRAY_STAINED_GLASS_PANE
    name: "§7边框"
```
