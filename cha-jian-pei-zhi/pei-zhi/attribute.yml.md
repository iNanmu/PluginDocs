---
description: 默认配置
---

# attribute.yml

## 属性配置

> 该配置 **并不代表最终插件生成的配置** 因为部分属性只有在插件加载后才生成
>
> 配置更新日期 **2024/11/12**

```yaml
options:
  lang: "zh_CN"
#通过插件API新注册的属性也会在此生成相对应节点的配置项
attribute:
  #属性名
  key:
    #攻击与防御类属性
    attackOrDefense:
      attack: "物理伤害"
    #更新类属性(即属性刷新时触发)
    update: {}
    #运行类属性(即每隔几秒触发一次)
    runtime: {}
    #其他类属性
    other: {}
  #优先级
  priority:
    attackOrDefense:
      attack: 1
    update: {}
    runtime: {}
  #属性值生效限制 (超过部分的属性值不生效,但还是可以读取并通过stats查看)
  value:
    attack: -1.0
  #战斗力
  combatPower:
    attackOrDefense:
      attack: 1.0
    update: {}
    runtime: {}
    other: {}
  #属性公式
  #{attackerAttack} 当前 被攻击者 所受伤害(受优先级影响)
  #{entityAttack} 当前 攻击者 所受伤害(受优先级影响)(例如反弹伤害)
  #{value} 取得对应属性值
  #{entityA:属性名} 取得攻击者的对应属性值
  #{entityB:属性名} 取得被攻击者的对应属性值
  formula: {}
  #消息
  message:
    #变量说明
    #{attacker} 攻击者名称
    #{entity} 被攻击者名称
    #{attackerDamage} 此次事件 被攻击者 所受最终伤害
    #{entityDamage} 此次事件 攻击者 所受最终伤害(例如反弹伤害)
    #{属性变量} 此次事件该属性所造成的属性值 (例 {attack})
    attack:
      - "对 {entityB} 造成 {attackerDamage} 点伤害,穿透伤害 {see_through}"
      - "{entityA} 对你造成 {attackerDamage} 点伤害"
    #特别提醒:
    #除 other 类属性外的所有属性点支持在这增加提示消息
    #节点名格式固定为属性变量名,例如
    #armor:
    #  - "对方抵消了你百分之 {armor} 点伤害!"
    #  - "你抵消了对方百分之 {armor} 点伤害!"
  #属性全息提示 (需开启 hologramMessage 功能)
  #前置 HolographicDisplays
  hologram:
    attack: "造成 {attackerDamage} 点物理伤害"
    #defense: "抵消 {defense} 点伤害"
    #属性变量: "内容"
  options:
    #冰冻属性持续时间
    frozenTime: 3
    #玩家闪避冷却间隔,每多少秒内仅允许闪避一次
    dodgeCooling: 0.0
    #吸血属性触发时额外造成吸血伤害(伤害等同吸血量)
    vampireDamage: true
    #默认移动速度
    defaultMoving: 0.25
    #默认生命力
    defaultHealth: 100.0
    #是否将生命心数锁定为两排
    #关闭该项可解决生命上限提升时受到的伤害抖动问题
    #关闭该项后上限提升的同时,生命心数也会变多(建议配合龙核、萌芽覆盖掉,不然挡屏甚至卡住客户端)
    healthScale: true
    #RUNTIME类属性的运行间隔(秒)
    runtimeAttributeTime: 5.0
    #生命力恢复间隔(秒)
    healthRestoreTime: 10.0
    #是否开启 HolographicDisplays 全息功能
    hologramMessage: false
    #防御系数(即 (PVE防御+PVP防御+防御力属性生效值的和) * 系数值)
    defenseCoefficient: 1.0
    #攻击系数(即 (PVE攻击+PVP攻击+攻击力属性生效值的和) * 系数值)
    attackCoefficient: 1.0

setting:
  #百分比读取属性格式的标志符
  #例如 "物理伤害: +100 (%)"
  percentageReadMark: "(%)"
  #限制属性加载包含下列其中描述的物品(会影响AttributeAPI附属加载属性)
  limit-attribute-descriptions:
    - "使物品属性失效"
  #禁止某行包含列表内字符的描述行加载属性
  limit-line-attribute-load:
    - "§f来源"
  #限制包含下列其中描述的物品在原版装备槽位中被加载属性(不会影响AttributeAPI附属加载属性)
  limit-slot-attribute-descriptions:
    - "无法在装备槽位中使用"
  #限制属性加载的世界
  limit-attribute-worlds:
    - "test_world"
  #加载指定NBT标签内属性列表
  attribute-nbt-list:
    - "attribute_tag"
  #加载物品属性时,根据物品名修正物品对应属性的最大值
  attribute-max-value-corrector:
    "对应的物品名": "战力评价=1000.0;属性名=200.0"
  #加载属性源时,根据属性源名修正属性源中对应属性的最大值
  #HAND/OFF_HAND/FEET/LEGS/CHEST/HEAD(SYSTEM) 对应原版槽位属性源名称
  attribute-max-value-corrector-source:
    "护手槽": "战力评价=1000.0;属性名=200.0"
  #权限限制
  #支持多个权限，例如 "职业: 剑士/法师/牧师" 只需要满足其一即可
  permission:
    split: "/"
    key: "职业"
  #装备等级限制
  level: "装备等级"
  #装备等级限制标签,等级来源变量
  level-placeholder: "%player_level%"
  #装备类型
  #例如 [装备类型: 双持]
  equipmentType:
    lore: "装备类型"
    list:
      - "双持"
      - "主手"
      - "副手"
      - "头盔"
      - "衣服"
      - "裤子"
      - "鞋子"
  options:
    #仅启用插件属性伤害 (关闭后 {attack} {overAttack} 也会附上其他插件的伤害数值)
    pluginDamage: false
    #原版伤害 (pluginDamage 为 true 时,此处默认 false)
    defaultDamage: true
    #原版护甲 (1.9+功能 原版护甲为百分比抵消伤害，会影响插件伤害的准确性，默认关闭)
    defaultArmor: true
    #开启后装备等级限制将根据玩家职业等级进行判断
    skillLevel: false
    #关闭后 SkillAPI 插件造成的技能伤害将不处理进行属性处理
    #3.3.0.1 版本过时,可使用 skill-options 内配置项
    skillDamage: true
    #关闭后  Magic 插件造成的技能伤害将不处理进行属性处理
    #3.3.0.1 版本过时,可使用 skill-options 内配置项
    magicDamage: true
    #技能兼容项
    #开启对应类型属性处理兼容后 SkillAPI/Magic 技能伤害将附上对应类型的属性处理
    skill-options:
      #攻击类属性兼容
      attack-attribute: true
      #防御类属性兼容
      defense-attribute: true
      #限制属性生效
      #在该列表内的属性触发技能伤害时不会生效处理
      prohibit-attribute: []
      #  - "闪避几率"
    #物品攻击检测
    attackDetection:
      #禁止物品左键攻击
      left-click:
        - "BOW"
      #远程伤害
      #只有在下列列表内的物品类型远程攻击才有伤害
      remote:
        - "BOW"
      #跳过 SkillAPI 技能伤害检测
      skill-damage-skip: true
      #跳过 Magic 技能伤害检测
      magic-damage-skip: true
      #被禁止时是否提示玩家
      message-enable: true
    mechanism:
      #支持版本: 1.9+
      #蓄力伤害机制(近战&远程都会受到影响)
      accumulateDamage: false
      #支持版本: 1.9+
      #盾牌格挡机制
      shield:
        enable: true
        #right 开启后盾牌就不再格挡,也不会冷却
        right: false
        #right 为 false 时启用盾牌格挡冷却机制
        cd: 10
      #支持版本 1.8? 1.9+
      #弓箭机制
      shoot:
        #弓箭属性计算公式均为 "属性值/100"
        enable: false
        #蓄力影响
        #拉满则可以打出满射速的箭,如果没拉满则按力道削弱速度
        #拉满精准度会提高,没拉满精准度则会降低,精准度不会超过 默认值+属性加成
        force: true
        #默认箭飞行速度 (数值越大速度越快)
        speed: 2.0
        #默认箭飞行偏离 (数值越大偏离越大)
        spread: 3.0
        #穿透 1.14+ 版本支持,其他版本爬
        through:
          #是否启用
          enable: false
          #穿透次数 (箭术穿透触发时穿透实体次数)
          amount: 3
      #MythicMobs 测试版本 4.7.2
      #MythicMobs 召唤继承
      #召唤的怪物会继承召唤者的某些属性
      summon:
        enable: false
        #可继承的怪物名字必须包含以下内容
        string: "[召唤]"
        #可继承的属性,不在列表内的属性不继承
        attribute:
          - "物理伤害"
      #触发器 ~onSignal:AttributePlus
      #兼容 MythicMobs 触发器 Signal 信号接收此次处理属性值列表
      #如果此次触发的属性处理不包括下面变量值属性则不触发该信号
      mythic-signal:
        #可在技能处理中使用 <skill.var.属性变量名(或自定义变量名)> 占位符获取此次攻击事件储存值
        #例如 <skill.var.attackerDamage|0(默认值)> 获取此次攻击事件造成的伤害值(AP攻击事件处理后的最终伤害)
        - attackerDamage
    entityAttribute:
      #实体属性刷新过滤
      filter:
        #原版怪物是否刷新时加载属性 (建议关闭,开启后所有为 LivingEntity 实体都会刷新属性)
        originalMonster: false
        #当 originalMonster 为 false 时启动
        #怪物名包含下列字符才刷新属性
        list:
          - "[怪物]"

```

{% hint style="info" %}
&#x20;MythicMobs 怪物属性相关，请 [查看此处](../../shu-xing-xiang-guan/mythicmobs-shu-xing-xiang-guan.md)
{% endhint %}
