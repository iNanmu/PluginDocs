# Interface (制作界面配置)

## 介绍

文件夹位置 **`./interface`**

该配置文件夹储存 **`自定义的制作界面`** 配置，可以自定义多个不同制作界面，以 **`锻造工艺界面`** 为例子:

{% code title="EXAMPLE.YML" %}
```yaml
name: "锻造界面"
title: "§f锻造界面"

layouts:
  - "#########"
  - "#I##@@@@#"
  - "####@@@@#"
  - "#P##@@@@#"
  - "#G##@@@@#"
  - "###S#A###"

materials:
  "I":
    type: "PHASE_INFO"
  "P":
    type: "MAKE_PRODUCT"
  "G":
    material: WHITE_STAINED_GLASS_PANE
    name: "§f提取锻造物"
    lore:
      - " "
      - "§f提取已锻造出来的物品"
      - "§f提取后将结束锻造"
      - " "
    type: "GET_MAKE_PRODUCT"
  #自动放入功能从 1.0.8 版本开始可使用
  "A":
    material: ORANGE_STAINED_GLASS_PANE
    name: "§f自动放入材料"
    lore:
      - " "
      - "§f点击自动将符合的材料"
      - "§f放置至界面中"
      - " "
    #自动放入材料
    type: "AUTO"
  "S":
    material: YELLOW_STAINED_GLASS_PANE
    name: "§f开始锻造"
    lore:
      - " "
      - "§f请放入材料后点击开始锻造"
      - "  §f共需锻造 §c{content *phase-size} §f阶段"
      - "  §f当前阶段需等待 §c{content *current-phase-time} §f秒"
      - " "
    type: "START_MAKE"
  "#":
    material: GRAY_STAINED_GLASS_PANE
    name: "§7边框"
```
{% endcode %}

## 进阶交互按钮玩法

该功能从 1.0.6 插件版本起新增，请跳转至 [工艺交互按钮](../gong-yi-jiao-hu-an-niu.md) 页面介绍
