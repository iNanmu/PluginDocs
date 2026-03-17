# 锻造示例

## MythicMobs 物品配置

你可以使用一下物品配置，配合该示例功能在游戏内亲身使用一次该功能，那能让你更好的理解改示例

可在游戏内通过 `/craft make 你的名字 楠木的帽子` 打开锻造界面

```yaml
皮革布料:
  Id: LEATHER
  Display: '&3皮革布料'
  Lore:
  - ' '
  - '&6&l* &7材料介绍'
  - '   &f* &7锻造 &6楠木的帽子 &7材料'
  - '   &f* &7材料为 &6第一阶段所需材料'
  - ' '
  - '&6&l* &7其他信息'
  - '   &f* &f+30% 锻造强度'

楠木的头皮屑:
  Id: 351
  data: 15
  Display: '&6楠木的头皮屑'
  Lore:
  - ' '
  - '&6&l* &7材料介绍'
  - '   &f* &7锻造 &6楠木的帽子 &7材料'
  - '   &f* &7该材料会在 §6楠木 §7挠头时掉落'
  - '   &f* &7材料为 &6第二阶段所需材料'

钻石之星:
  Id: DIAMOND
  Display: '&6钻石之星'
  Lore:
  - ' '
  - '&6&l* &7材料介绍'
  - '   &f* &7锻造 &6楠木的帽子 &7材料'
  - '   &f* &7放入该材料第二阶段锻造后会将'
  - '   &f* &7帽子材质提升为 §b钻石'
```

## 锻造示例

```yaml
#项目名
content-name: "楠木的帽子"
#项目所属分类
class: "锻造类目"
#项目所使用的界面
interface: "锻造界面"
#提取后关闭界面返回该图纸制作界面
#关闭该项后提取物品关闭界面时会返回 正在制作的工艺 界面
extract-return: true
#默认学会图纸 (默认学习会是 1 级)
default-learn: true
#显示优先级
show-priority: 1

#项目品质(每次开始制作项目时随机获取一个品质)
quality:
  "史诗": 10.0
  "良好": 50.0
  "普通": 100.0

#描述,可使用 $[计算公式] 例如 $[公式 *int/double]
describes:
  "基础锻造信息":
    - " "
    - "&6&l† &7基础属性"
    - "   &f▪ &f品质: &c@品质"
    - "   &f▪ &f评分: &c@评分"
    - " "
    - "&6&l† &7基础属性"
    #该行使用 $[计算公式] 计算公式,计算锻造强度加成计算
    - "   &f▪ &f物理伤害 &c+$[{random *r:10-500 *0.1}*(1.0+({data *锻造强度 *0.0}/100.0)) *double]"
    - "   &f▪ &f{random *rs:暴击几率,吸血几率 *10.0,8.0} &c+{random *r:1-5 *5.0}%"
    - " "
  "普通属性":
    - "&6&l† &7灵魂加成"
    - "   &f▪ &f物理伤害 &c+{random *r:30-100 *0.1}"
    - "   &f▪ &f暴击几率 &c+1%"
  "良好属性":
    - "&6&l† &7灵魂加成"
    - "   &f▪ &f物理伤害 &c+{random *r:50-200 *0.1}"
    - "   &f▪ &f暴击几率 &c+3%"
  "史诗属性":
    - "&6&l† &7灵魂加成"
    - "   &f▪ &f物理伤害 &c+{random *r:100-300 *0.1}"
    - "   &f▪ &f暴击几率 &c+10%"

#制作阶段
phases:
  1:
    #阶段制作耗时
    time: 600
    #完成该阶段时是否可以提取该阶段制作的物品
    extract: true
    #阶段制作材料
    materials:
      1:
        name: "§3皮革布料"
        must: true
        amount: 1
        display: "皮革布料"
        #数据名
        #放入材料后可以提供 material-data 或 material-central 占位符获取数据
        data: "皮革布料"
    #阶段制作介绍
    introduce:
      material: BOOK
      name: "§f干净的帽子"
      lore-displays:
        1:
          lore:
            - " "
            - "&6&l† &7基础属性"
            - "   &f▪ &f品质: &c@品质"
            - "   &f▪ &f评分: &c@评分"
            - " "
            - "&6&l† &7基础属性"
            #该行使用 $[计算公式] 计算公式,计算锻造强度加成计算
            - "   &f▪ &f物理伤害 &c+(10-100)"
            - "   &f▪ &f暴击几率/吸血几率 &c+(1-5)%"
            - " "
    #启动制作动作(设置 cancel 则取消制作)
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
    extract-actions:
      1:
        - meet:
            #替换锻造物上的 @品质、评分 占位符
            - "craft:describe *replace-text *@品质 *{quality}"
            - "craft:describe *replace-text *@评分 *{score}"
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
