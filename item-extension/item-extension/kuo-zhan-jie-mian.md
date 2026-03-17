# 扩展界面

## 说明

扩展界面可以 **自定义布局、自定义允许放入的扩展道具识别符** 通过改功能你可以将不同玩法的界面

进行区分，同时 **支持翻页** 功能

## 配置

该配置为 **宝石镶嵌** 示例配置，你可以在 [扩展示例](kuo-zhan-shi-li/) 中找到相关配置

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
