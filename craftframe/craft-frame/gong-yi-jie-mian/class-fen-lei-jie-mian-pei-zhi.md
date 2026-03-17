# Class (分类界面配置)

## 介绍

文件夹位置 **./class**

该配置文件夹储存 **自定义的分类界面** 配置，可以自定义多个不同分类界面，以 **锻造分类界面** 为例子:

一看就懂，所以不详细介绍，示例配置内已添加注释

{% code title="EXAMPLE.YML" %}
```yaml
#分类名称
class-name: "锻造类目"

#界面名
title: "§f你已学习的锻造图纸"
#布局内 @ 占位符代表玩家学习的工艺,以工艺的熟练度从高到低显示
layouts:
  - "#########"
  - "#@@@@@@@#"
  - "##P###N##"

#布局材料
materials:
  "#":
    material: GRAY_STAINED_GLASS_PANE
    name: "§7边框"
  "P":
    material: PAPER
    name: "§7上一页"
  "N":
    material: PAPER
    name: "§7下一页"

#工艺图纸介绍
#该类目界面内显示工艺图纸的物品
drawings-introduce:
  material: PAPER
  name: "§6@content §f图纸"
  lore:
    - "§f你当前对 §6@content §f图纸的信息"
    - " "
    - "  §f学习等级 §c@level"
    - "  §f制作熟练度 §c@proficiency"
    - " "
    - "§a点击锻造该图纸"

#制作界面内正在制作的工艺物品介绍
make-introduce:
  material: ANVIL
  name: "§f正在锻造 §6{content} §f物品"
  lore:
    - " "
    - " §f锻造阶段 §c{content *current-phase-size}§f/§c{content *phase-size}"
    - " "
    - "§f该阶段将在 §6{content *run-phase-time} §f时完成"

#制作界面内新一阶段还未开始制作工艺时显示的物品
make-stop-introduce:
  material: ANVIL
  name: "§f锻造 §6{content} §f物品"
  lore:
    - " "
    - " §f锻造阶段 §c{content *current-phase-size}§f/§c{content *phase-size}"
    - " §f当前品质 §3{quality}"
    - " §f当前评分 §3{score}"
    - " "
    - "§a点击继续锻造"

#主分类界面上的物品,即 /craft class 命令打开的界面
class-introduce:
  material: ANVIL
  name: "§f锻造分类"
  lore:
    - " "
    - "§f点击打开 §6锻造 §f界面"
    - " "
```
{% endcode %}
