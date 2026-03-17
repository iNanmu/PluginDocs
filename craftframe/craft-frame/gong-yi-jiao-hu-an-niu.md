---
description: 进阶玩法
---

# 工艺交互按钮

## 交互按钮

该功能是 [`工艺制作界面的扩展教程(Interface)`](gong-yi-jie-mian/interface-zhi-zuo-jie-mian-pei-zhi.md) 即你可以在 `工艺制作界面` 上添加交互按钮，玩家打开制作界面后可点击不同类型的交互按钮，交互按钮玩家交互后的数据值可在工艺制作脚本内通过 [`Data`](gong-yi-zhan-wei-fu/data.md#shu-ju-du-qu) 占位符进行获取，让插件的自定义性更上一层

## 交互类型

在交互按钮物品编写上，可以使用 `{mode_value}` 占位符获取玩家交互的数据

所有按钮效果视频 [https://reccloud.cn/u/7ayf1ao](https://reccloud.cn/u/7ayf1ao) (仅按钮效果展示)

回收示例效果视频 [https://reccloud.cn/u/oh6ju4c](https://reccloud.cn/u/oh6ju4c) (1.0.6插件自带示例配置效果)

{% tabs %}
{% tab title="多项单选按钮" %}
该按钮点击可以切换下一项，右键切换上一项，可预先设置不同选项供玩家选择

具体配置如下

<pre class="language-yaml"><code class="lang-yaml"><strong>materials:
</strong>  #"...": ...
  "M":
    material: GREEN_STAINED_GLASS_PANE
    name: "§6回收为 §f{mode_value}"
    lore:
      - "§6左键 §f/ §6右键 §f切换"
      - "§f金币回收价值比例 §61:1"
      - "§f点券回收价值比例 §61:0.3"
      - "§f"
    #选择模式
    type: "SELECT_MODE"
    #数据储存KEY,在工艺制作时可通过 data 占位符获取玩家选项数据
    #例如 {data *回收模式}
    data: "回收模式"
    #默认值
    default: "金币"
    #选项列表
    options:
      - "金币"
      - "点券"
</code></pre>
{% endtab %}

{% tab title="取值按钮" %}
该按钮 `左键取值+1、右键取值-1` 如果按住 SHIFT 键则 `+10、-10`&#x20;

具体配置如下

<pre class="language-yaml"><code class="lang-yaml"><strong>materials:
</strong>  #"...": ...
  "M":
    material: GREEN_STAINED_GLASS_PANE
    name: "§6回收数量 §f{mode_value}"
    lore:
      - "§6左键 §f+1 §7(SHIFT +10)"
      - "§6右键 §f-1 §7(SHIFT -10)"
    #取值模式
    type: "VALUE_MODE"
    #数据储存KEY,在工艺制作时可通过 data 占位符获取玩家选项数据
    #例如 {data *取值}
    data: "取值"
    #默认值
    default: 1
</code></pre>
{% endtab %}

{% tab title="复选按钮" %}
该按钮点击后切换状态，分别为 true、false 两个状态

具体配置如下

<pre class="language-yaml"><code class="lang-yaml"><strong>materials:
</strong>  #"...": ...
  "M":
    material: GREEN_STAINED_GLASS_PANE
    name: "§6是否使用加成卷 §f{mode_value}"
    lore:
      - "§6左键 §f/ §6右键 §f切换"
    #复选模式
    type: "CHECK_MODE"
    #数据储存KEY,在工艺制作时可通过 data 占位符获取玩家选项数据
    #例如 {data *复选状态}
    data: "复选状态"
    #默认值
    default: false
</code></pre>
{% endtab %}
{% endtabs %}

完整的配置示例，切勿直接复制，仅用于教程，具体效果可以看下方视频

```yaml
name: "回收界面"
title: "§f物品回收"

layouts:
  - "@@@@@@@@@"
  - "@@@@@@@@@"
  - "@@@@@@@@@"
  - "#C#M#V#S#"

materials:
  "I":
    type: "PHASE_INFO"
  "S":
    material: GREEN_STAINED_GLASS_PANE
    name: ""
    lore:
      - "§f放入包含&6物品价值&f的物品"
      - "     &a&l点击开始回收"
      - " "
    type: "START_MAKE"
  "M":
    material: GREEN_STAINED_GLASS_PANE
    name: "§6回收为 §f{mode_value}"
    lore:
      - "§6左键 §f/ §6右键 §f切换"
      - "§f金币回收价值比例 §61:1"
      - "§f点券回收价值比例 §61:0.3"
      - "§f"
    #选择模式
    type: "SELECT_MODE"
    #数据储存KEY
    #在工艺制作时可通过 data 占位符获取玩家选项数据
    data: "回收模式"
    #默认值
    default: "金币"
    #选项列表
    options:
      - "金币"
      - "点券"
  "C":
    material: GREEN_STAINED_GLASS_PANE
    name: "§6回收数量 §f{mode_value}"
    lore:
      - "§6左键 §f+1 §7(SHIFT +10)"
      - "§6右键 §f-1 §7(SHIFT -10)"
    type: "VALUE_MODE"
    data: "取值"
    default: 1
  "V":
    material: GREEN_STAINED_GLASS_PANE
    name: "§6是否使用加成卷 §f{mode_value}"
    lore:
      - "§6左键 §f/ §6右键 §f切换"
    type: "CHECK_MODE"
    data: "复选状态"
    default: false
  "#":
    material: GRAY_STAINED_GLASS_PANE
    name: "§7边框"
```
