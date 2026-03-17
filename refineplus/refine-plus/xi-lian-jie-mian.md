# 洗练界面

## 前言

洗练界面可以有多个不同的布局，洗练界面布局完全自定义，洗练界面配置位于 **./view** 文件夹中，一个完整的 [洗练界面](xi-lian-jie-mian.md#undefined) 示例

## 界面布局

这个没什么好说的，主要还是得说 [界面物品配置(标识符)](xi-lian-jie-mian.md#jie-mian-wu-pin-pei-zhi)

```yaml
#界面标题
title: "普通洗练"
#界面布局，标识符必须再 view-material 上配置
view-slots:
  - BBBBBBBBB
  - B*******B
  - BBBBBBBBB
  - BBBBRBBBB
  - BBBBBBLBB
  - BBBBYBBBB
#界面物品
view-material:
  ...
```

## 界面物品配置

### 基础配置

<table><thead><tr><th>配置项</th><th>说明</th><th>例子</th></tr></thead><tbody><tr><td>type (必填)</td><td><a href="xi-lian-jie-mian.md#undefined">处理类型</a></td><td>type: <strong>border</strong></td></tr><tr><td>update</td><td>槽位更新 (开启后将实时更新物品描述等信息)</td><td>update: <strong>false</strong></td></tr><tr><td>items-returned</td><td>物品返回 (关闭界面时自动返回槽位上放置的物品)</td><td>items-returned: <strong>false</strong></td></tr><tr><td>name (必填)</td><td>物品名</td><td>name: <strong>"边框"</strong></td></tr><tr><td>lore (必填)</td><td>物品描述，支持<a href="xi-lian-jie-mian.md#zhan-wei-fu">占位符</a></td><td><pre class="language-yaml"><code class="lang-yaml"> lore:
   - "&#x26;7边框 | 无法点击"
</code></pre></td></tr></tbody></table>

### 处理类型

| 类型       | 说明                      |
| -------- | ----------------------- |
| border   | 边框槽 (无法点击)              |
| refine   | 洗练物品槽 (可放入/取出)          |
| material | 洗练材料放置槽 (可放入/取出)        |
| lock     | 条词锁定操作按钮槽 (左键/右键/SHIFT) |
| confirm  | 确定按钮槽 (点击开始洗练)          |

```yaml
view-material:
  #标识符
  "B":
      #类型
    - type: border
      #物品类型
      material: "STAINED_GLASS_PANE:15"
      #物品名
      name: "&8边框"
      #物品描述
      lore:
        - "&7边框 | 无法点击"
  "L":
    - type: lock
      update: true
      material: "STAINED_GLASS_PANE:4"
      name: "&8条词锁定"
      lore:
        - "&7左键: 上一行"
        - "&7右键: 下一行"
        - "&7Shift键+点击: 切换锁定状态"
        - ""
        - "&7当前物品洗练属性: "
        - "&7{attributes}"
  "Y":
    - type: confirm
      update: true
      material: "STAINED_GLASS_PANE:5"
      name: "&6开启洗练"
      lore:
        - "&7确定 | 点击开始洗练"
        - "&7当前洗练次数: &c{refine-number}"
        - " "
        - "&7{required-material}"
  "R":
    - type: refine
      #关闭界面时自动返回槽位上的物品
      items-returned: true
      material: "STAINED_GLASS_PANE:6"
      name: "&6装备槽"
      lore:
        - "&7装备 | 将洗练装备放入"
        - "&7当前洗练次数: &c{refine-number}"
  "*":
    - type: material
      items-returned: true
      material: "STAINED_GLASS_PANE:8"
      name: "&6洗练材料"
      lore:
        - "&7材料 | 将洗练所需材料放入"
```

## 占位符

| 占位符                 | 说明                |
| ------------------- | ----------------- |
| {required-material} | 本次洗练所需消耗的必备材料及数量  |
| {attributes}        | 物品的洗练属性 (配合锁词条显示) |
| {chance}            | 本次洗练成功几率          |
| {aegis}             | 是否已使用保护道具         |
| {refine-number}     | 物品已洗练的次数          |

## Example.yml

```yaml
#界面标题
title: "普通洗练"

#通过该界面洗练的顶部、底部描述 (没有设置则使用 config 默认配置)
refine-info:
  #顶部描述 (不可为空白)
  top: "&f&m&l--------&f[&6&l洗练属性&f]&f&m&l--------"
  #底部描述 (不可为空白)
  bottom: "&f&m&l--------&f[&6&l洗练属性&f]&f&m&l--------"
  
#界面位置布局
view-slots:
  - BBBBBBBBB
  - B*******B
  - BBBBBBBBB
  - BBBBRBBBB
  - BBBBBBLBB
  - BBBBYBBBB
#界面布局材料
view-material:
  "B":
    - type: border
      material: "STAINED_GLASS_PANE:15"
      name: "&8边框"
      lore:
        - "&7边框 | 无法点击"
  "L":
    - type: lock
      update: true
      material: "STAINED_GLASS_PANE:4"
      name: "&8条词锁定"
      lore:
        - "&7左键: 上一行"
        - "&7右键: 下一行"
        - "&7Shift键+点击: 切换锁定状态"
        - ""
        - "&7当前物品洗练属性: "
        - "&7{attributes}"
  "Y":
    - type: confirm
      update: true
      material: "STAINED_GLASS_PANE:5"
      name: "&6开启洗练"
      lore:
        - "&7确定 | 点击开始洗练"
        - "&7当前洗练次数: &c{refine-number}"
        - " "
        - "&7{required-material}"
  "R":
    - type: refine
      #关闭界面时自动返回槽位上的物品
      items-returned: true
      material: "STAINED_GLASS_PANE:6"
      name: "&6装备槽"
      lore:
        - "&7装备 | 将洗练装备放入"
        - "&7当前洗练次数: &c{refine-number}"
  "*":
    - type: material
      items-returned: true
      material: "STAINED_GLASS_PANE:8"
      name: "&6洗练材料"
      lore:
        - "&7材料 | 将洗练所需材料放入"
```
