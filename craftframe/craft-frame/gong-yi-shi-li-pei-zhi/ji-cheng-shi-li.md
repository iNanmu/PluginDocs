# 继承示例

## MythicMobs 物品配置

你可以使用一下物品配置，配合该示例功能在游戏内亲身使用一次该功能，那能让你更好的理解改示例

可在游戏内通过 `/craft make 你的名字 继承重铸属性` 打开继承界面

```yaml
勇士之剑:
  Id: 267
  Display: '&6勇士之剑'
  Lore:
  - ' '
  - '&6&l* &f可重铸'
  - ' '
  - '&6&l* &7基础属性'
  - '   &f* &7物理伤害&f: 5 - 10'
  - '   &f* &7暴击几率&f: 10 %'
  - '   &f* &7暴击伤害&f: 50 %'
  - ' '
  - '&6&l* &7重铸属性'
  - '   §*§f* &f物理伤害 &f+&c100'
  - '   §*&c* &f暴击几率 &f+&c10%'
  - '   §*&4* &f暴击伤害 &f+&c300%'
  - ' '
  
勇士之剑-2:
  Id: 267
  Display: '&6勇士之剑'
  Lore:
  - ' '
  - '&6&l* &f不可重铸'
  - ' '
  - '&6&l* &7基础属性'
  - '   &f* &7物理伤害&f: 5 - 10'
  - '   &f* &7暴击几率&f: 10 %'
  - '   &f* &7暴击伤害&f: 50 %'
  - ' '
  - '&6&l* &7重铸属性'
  - '   §*§f* &f物理伤害 &f+&c10'
  - '   §*&c* &f暴击几率 &f+&c1%'
  - '   §*&4* &f暴击伤害 &f+&c30%'
  - ' '
  
继承石:
  Id: DIAMOND
  Display: '&6继承石'
  Lore:
  - ' '
  - '&6&l* &7材料介绍'
  - '   &f* &7继承任意装备时可选材料'
  - '   &f* &7该材料可开启 &6继承宝箱 &7获得'
  - ' '
  - '&6&l* &7材料加成'
  - '   &f* &f+10% 继承概率'
  - ' '
```

## 继承示例

```yaml
content-name: "继承重铸属性"
class: "继承类目"
interface: "继承界面"

phases:
  1:
    time: 10
    materials:
      1:
        #放入的材料必须包含能匹配上的 §7重铸属性 描述
        #如果要限制物品名,请改用 name: "名称"
        lore: "§7重铸属性"
        must: true
        amount: 1
        display: "继承物"
        data: "继承物"
      2:
        lore: "§7重铸属性"
        must: true
        amount: 1
        display: "被继承物"
        data: "被继承物"
      3:
        name: "§6继承石"
        must: false
        display: "继承石"
        data: "继承石"
    introduce:
      material: IRON_SWORD
      name: "§f继承重铸属性"
      lore-displays:
        1:
          lore:
            - " "
            - "&f▪ &f继承成功概率 &c50 &f%"
            - " "
            - "&f▪ &f继承成功后将为 &6继承物 &f继承"
            - "&f▪ &6被继承物 &f上的 &6重铸属性"
            - " "
            - "&f▪ &6被继承物 &f无论是否继承成功都会 &c消失"
            - " "
    start-actions:
      1:
        - condition:
            #判断放入的 继承物 是否已经继承过 2 次
            - "check '{material-data *继承物 *get-nbt *继承次数 *0}' == 2"
          meet:
            - "send '&f你放入的继承物无法继续继承,继承次数已达到 2 次 ({material-data *继承物 *get-nbt *继承次数 *0})'"
            - "cancel_all"
      2:
        - meet:
            #设置默认重铸概率
            - "craft:data *继承概率 *add *50.0"
            #读取所有放入的材料上 "+(.*?)% 继承概率" 上的概率值 (该读取最终还会乘以放入的材料数量)
            - "craft:data *继承概率 *add *{material-central *lore-value *+(.*?)% 继承概率}"
    actions:
      #主动作组
      1:
        #子动作组
        1:
          - condition:
              #模拟重铸概率,并判断是否放入的保护符
              - "check random 100 <= {data *继承概率 *50.0}"
            meet:
              #重铸概率判断通过,取消该主动作组内所有子动作组运行
              #这里的 cancel_sub 跟 cancel_all 区别在于 cancel_sub 只作用于子动作组内,而 cancel_all为所有动作组
              - "cancel_sub"
            not-meet:
              #发送消息
              - "send '&f你在继承物品 &6重铸属性 &f时发生炸炉,毁于一旦 ({data *继承概率 *50.0})'"
              #将 继承物 原封不动的复制回去
              - "craft:describe *copy-material *继承物"
              #结束制作并提取物品
              - "craft:system *extract-stop"
              #取消接下来的所有动作组运行
              - "cancel_all"
      2:
        1:
          - meet:
              #复制 继承物 物品原数据上的 类型、数量、名称、描述 等数据
              - "craft:describe *copy-material *继承物"
              #使用 "describe *replace-part-line *起始行(非模糊匹配) *结束行(非模糊匹配) *描述" 方法
              #将 继承物 上的指定范围内的描述,替换为 被继承物 上指定范围内的描述
              - "craft:describe *replace-part-line *&6&l* &7重铸属性 *  *{material-data *被继承物 *plugin-part-lores *&6&l* &7重铸属性 * }"
              #使用NBT储存为继承物的继承次数NBT数据加上一次继承记录,利用到计算公式占位符
              - "craft:nbt *set *继承次数 *int *$[1 + {material-data *继承物 *get-nbt *继承次数 *0} *int]"

material-displays:
  "继承物":
    material: BARRIER
    name: "§6继承的物品"
    lore:
      - " "
      - "&f▪ &f请放入描述包含 §6重铸属性 §f的物品"
      - "&f▪ &f继承失败会返回原继承物"
      - " "
  "被继承物":
    material: BARRIER
    name: "§6被继承的物品"
    lore:
      - " "
      - "&f▪ &f请放入描述包含 §6重铸属性 §f的物品"
      - "&f▪ &f无论是否继承成功,该物品都会 §c消失"
      - " "
  "继承石":
    material: BARRIER
    name: "§6继承石"
    lore:
      - " "
      - "&f▪ &f继承任意装备时需放入该材料"
      - " "
```
