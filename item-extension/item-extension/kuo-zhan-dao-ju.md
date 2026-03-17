# 扩展道具

## 说明

扩展道具即镶嵌到装备扩展位上的道具，可为玩家提供 **属性、技能** 等效果

## 全局设置

```yaml
#全局设置
global:
  #扩展位标识符,不过滤颜色代码
  #即在装备上写 方形 两个字即可被识别为扩展位
  identify: "方形"

  #扩展数量限制,默认为 -1 无限制
  #即一件装备仅允许使用几个该道具
  number: 3

  #全局放置条件设置
  condition:
    - kether...

  #全局放置动作设置
  #即向装备扩展位放置该配置下的所有道具均会触发
  wear-action:
    - kether...
    
  #全局拆除动作设置
  #即向装备扩展位拆除该配置下的所有道具均会触发
  tear-action:
    - kether...
  
  #全局属性设置
  attribute:
    - "物理伤害: 100"
    
  #全局技能设置
  skill:
    - "技能名"

  #扩展道具
  #即通过 ie give 命令获取的物品
  display:
    material: DIAMOND
    name: "§6力量宝石 §fLv.{level}"
    lore:
      - " §f扩展位置: §6方§6形"
```

## 道具等级

不同道具等级可设置不同的属性、技能效果，此处的配置优先级大于 **全局设置** 即这里如果没有设置对应

的配置项，则以 **全局设置** 为主，如果设置的话则以 **道具等级** 内的配置为主

```yaml
levels:
  #等级
  1:
    #扩展后显示在装备上的内容
    show: "§6力量I"

    #设置该等级扩展道具的 custom-module-data 值
    #custom-module-data: 0

    #放置数量限制,默认为 -1 无限制
    #这里的限制优先级大于 全局设置 的限制
    number: 1    
    
    #是否允许拆除 (默认允许)
    dismantle: true
    
    #拆除是否返还宝石(默认返还)
    dismantle-return-props: true

    #扩展道具属性
    attribute:
      - "物理伤害: 20-50"
    
    #扩展道具技能
    #需要在 extension-skill 文件夹内配置对应技能
    skill:
      - "技能名"
      
    #放置条件设置
    condition:
      - kether...
    
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
```

## 套装配置

每个扩展道具配置都可以设置套装，玩家为身上装备扩展多少个该扩展道具激活对应的 **属性、技能**

这里的数量是以 **玩家全身装备上所安装的该扩展道具的数量**

```yaml
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
    skill:
      - "技能名"
```

## 完整的配置

该配置为 **宝石镶嵌** 示例配置，你可以在 [扩展示例](kuo-zhan-shi-li/) 中找到相关配置

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
  #放置条件设置
  condition:
    # ie-item contains {name/lore/type} array [ params ] 模糊匹配对应类型数据
    - check {{ ie-item contains lore array [ "§f装备类型 §6主武器" "§f装备类型 §6副武器" ] }} == 'true'

levels:
  1:
    #扩展后显示在装备上的内容
    show: "§6力量I"
    #扩展道具属性
    attribute:
      - "物理伤害: 20-50"
    #设置该等级扩展道具的 custom-module-data 值
    #custom-module-data: 100
    #是否允许拆除(默认允许)
    #dismantle: true
    #拆除是否返还宝石(默认返还)
    #dismantle-return-props: false
    #放置条件设置(优先级大于 global 所设条件)
    #condition:
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
