# 工艺阶段

## 介绍

每个工艺配置都可设置多个制作阶段，每个阶段可以设置放入不同的工艺制作材料，同时不同的阶段制作时长，改阶段还是以 物品锻造 的配置为例

## 工艺阶段

可能比较复杂，但注释比较详细，慢慢看总能看会

```yaml
#制作阶段
phases:
  #第一阶段
  1:
    #阶段制作耗时
    time: 600
    #完成该阶段时是否可以提取该阶段制作的物品
    extract: true
    #阶段制作材料
    materials:
      #1号材料
      1:
        #玩家放入材料时检测物品名模糊匹配判断
        #lore: "描述模糊匹配",与 name 相同,但判断的是描述
        #type: "材料类型匹配" 支持使用 ',' 区分多个
        name: "§3皮革布料"
        #是否为必须材料
        must: true
        #所需数量 (设-1或删除则不限制放入数量)
        amount: 1
        #在工艺制作界面上显示的物品数据
        #工艺图纸介绍页面内的 material-displays 配置项内容
        display: "皮革布料"
        #工艺材料数据储存KEY
        #放入材料后可以提供 material-data 或 material-central 占位符获取数据
        data: "皮革布料"
    #阶段制作介绍 (会显示再工艺制作界面上起到说明作用)
    introduce:
      material: BOOK
      name: "§f干净的帽子"
      lore-displays:
        #描述显示步骤1
        1:
          #这里可以加判断,判断通过下面 Lore 才会显示出来
          #condition:
          #  - "XXX"
          lore:
            - " "
            - "&6&l† &7基础属性"
            - "   &f▪ &f品质: &c@品质"
            - "   &f▪ &f评分: &c@评分"
            - " "
            - "&6&l† &7基础属性"
            - "   &f▪ &f物理伤害 &c+(10-100)"
            - "   &f▪ &f暴击几率/吸血几率 &c+(1-5)%"
            - " "
        #可以有描述显示步骤 2 与上方配置格式相同
        #2: ...
    #启动制作动作(设置 cancel_all 则取消制作,不会消耗材料)
    #该位置触发的时候就已经可以显示获取到材料数据
    start-actions:
      1:
        - condition:
            - "check '%player_level%' >= 10"
          meet:
            #读取所有放入的材料上 "+(.*?)% 锻造强度" 上的强度值,用于加强基础属性伤害
            - "craft:data *锻造强度 *add *{material-central *lore-value *+(.*?)% 锻造强度}"
          no-meet:
            #不满足条件发送提示
            - "send '你的等级不满 10 级,无法锻造该物品'"
            #停止制作处理
            - "cancel_all"
    #制作等待时间完成后运行动作
    actions:
      #主动作组
      1:
        #子动作组
        1:
          - condition:
              #检测放入的 "§6皮革布料" 的材料,名字是否包含 史诗 包含则设置此次制作物的品质为 史诗
              - "check '{material-data *皮革布料 *name-contains *史诗}' == true"
            meet:
              #设置此次制作物品质为史诗
              - "craft:quality *史诗"
        2:
          - condition:
              #与上方相同
              - "check '{material-data *皮革布料 *name-contains *良好}' == true"
            meet:
              - "craft:quality *良好"
        3:
          - meet:
              #设置制作物物品类型(皮革帽)
              - "craft:type *LEATHER_HELMET"
              #设置制作物成品的名字
              - "craft:name *§f干净的帽子"
              #为制作物添加 基础属性 描述,上方 describes 配置预设
              - "craft:describe *add *基础锻造信息"
    #提取物品时触发动作
    #该阶段上方设置 extract 为true,即玩家可以选择锻造第二阶段,也可以选择
    #提取这一阶段已制作出来的物品
    extract-actions:
      1:
        - meet:
            #替换锻造物上的 @品质、评分 占位符
            - "craft:describe *replace-text *@品质 *{quality}"
            - "craft:describe *replace-text *@评分 *{score}"
  #上面属于第一阶段的制作,下面可以写安装 1 2 3 依次写阶段
  #第二阶段
  #放入 "§6楠木的头皮屑" 材料,新增锻造属性
  2:
    time: 10
    #阶段制作材料
    materials:
      1:
        name: "§6楠木的头皮屑"
        must: true
        amount: 5
        display: "头皮屑材料"
      2:
        name: "§6钻石之星"
        must: false
        amount: 1
        display: "钻石之星"
        data: "钻石之星"
    introduce:
      material: BOOK
      name: "§6楠木的帽子"
      lore-displays:
        1:
          lore:
            - " "
            - "&6&l† &7灵魂附加"
            - "   &f▪ &f放入 &6楠木的头皮屑 &f为帽子"
            - "   &f▪ &f注入 &6灵魂加成"
            - " "
        2:
          condition:
            - "check '{quality}' == '史诗'"
          lore:
            - "&6&l† &7灵魂加成"
            - "   &f▪ &f物理伤害 &c+(100-300)"
            - "   &f▪ &f暴击几率 &c+10%"
        3:
          condition:
            - "check '{quality}' == '良好'"
          lore:
            - "&6&l† &7灵魂加成"
            - "   &f▪ &f物理伤害 &c+(50-200)"
            - "   &f▪ &f暴击几率 &c+3%"
        4:
          condition:
            - "check '{quality}' == '普通'"
          lore:
            - "&6&l† &7灵魂加成"
            - "   &f▪ &f物理伤害 &c+(30-100)"
            - "   &f▪ &f暴击几率 &c+1%"
    actions:
      1:
        1:
          - condition:
              #检测是否放入 钻石之星 材料
              - "check '{material-central *key-contains *钻石之星}' == true"
            meet:
              #修改材质并修改锻造物名
              - "craft:type *DIAMOND_HELMET"
              - "craft:name *§6楠木的帽子"
            not-meet:
              #仅修改锻造物名
              - "craft:name *§6楠木的帽子"
        2:
          - condition:
              #判断锻造物品质并赋予相同品质的属性值
              - "check '{quality}' == '史诗'"
            meet:
              - "craft:describe *add *史诗属性"
        3:
          - condition:
              - "check '{quality}' == '良好'"
            meet:
              - "craft:describe *add *良好属性"
        4:
          - condition:
              - "check '{quality}' == '普通'"
            meet:
              - "craft:describe *add *普通属性"
    extract-actions:
      1:
        - meet:
            #替换锻造物上的 @品质、评分 占位符
            - "craft:describe *replace-text *@品质 *{quality}"
            - "craft:describe *replace-text *@评分 *{score}"

#这个就是上面阶段工艺材料上 display 所设内容,会根据设置在制作界面上显示材料介绍
material-displays:
  "皮革布料":
    material: BARRIER
    name: "§3皮革布料 §cx §f1"
    lore:
      - " "
      - "  §f锻造 §6楠木的帽子 §f所需材料"
      - "  §f第一阶段材料"
      - " "
  "头皮屑材料":
    material: BARRIER
    name: "§6楠木的头皮屑 §cx §f5"
    lore:
      - " "
      - "  §f锻造 §6楠木的帽子 §f所需材料"
      - "  §f该材料会在 §6楠木 §f挠头时掉落"
      - "  §f第二阶段材料"
      - " "
  "钻石之星":
    material: BARRIER
    name: "§6钻石之星 §cx §f1"
    lore:
      - " "
      - "  §f锻造 §6楠木的帽子 §f可选材料"
      - "  §f放入该材料第二阶段锻造后会将"
      - "  §f帽子材质提升为 §b钻石"
      - " "
```

看完上方的例子配置，可能你还有点迷糊，所以我建议你加载插件，去亲自使用下 锻造 的这个例子配置，那样子能更好的理解原理，不迷糊就当我没说
