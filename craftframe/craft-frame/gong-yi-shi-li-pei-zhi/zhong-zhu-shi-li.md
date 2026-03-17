# 重铸示例

## MythicMobs 物品配置

你可以使用一下物品配置，配合该示例功能在游戏内亲身使用一次该功能，那能让你更好的理解改示例

可在游戏内通过 `/craft make 你的名字 勇士之剑` 打开重铸界面

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
  - '   §*§f* &f物理伤害 &f+&c10'
  - '   §*&c* &f暴击几率 &f+&c1%'
  - '   §*&4* &f暴击伤害 &f+&c30%'
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
```

## 重铸示例

```yaml
content-name: "勇士之剑"
class: "重铸类目"
interface: "重铸界面"

describes:
  "物理属性重铸":
    - "   §*&f* &f物理伤害 +$[{random *r:10-500 *0.1}*(1.0+({data *重铸强度 *0.0}/100.0)) *double]"
  "暴击几率重铸":
    - "   §*&c* &f暴击几率 +$[{random *r:1-10 *1.0}*(1.0+({data *重铸强度 *0.0}/100.0)) *double]"
  "暴击伤害重铸":
    - "   §*&4* &f暴击伤害 +$[{random *r:30-150 *0.5}*(1.0+({data *重铸强度 *0.0}/100.0)) *double]"

phases:
  1:
    time: 10
    materials:
      1:
        name: "§6勇士之剑"
        must: true
        amount: 1
        display: "勇士之剑"
        data: "勇士之剑"
      2:
        name: "§6重铸石"
        must: true
        display: "重铸石"
        data: "重铸石"
      3:
        name: "§6重铸保护符"
        amount: 1
        must: false
        display: "重铸保护符"
        data: "重铸保护符"
    introduce:
      material: IRON_SWORD
      name: "§f重铸 §6勇士之剑"
      lore-displays:
        1:
          lore:
            - " "
            - "&f▪ &f重铸成功概率 &c20 &f%"
            - " "
            - "&6&l* &7重铸属性"
            - "   §*§f* &f物理伤害 &f+&c(10-500)"
            - "   §*&c* &f暴击几率 &f+&c(1-10)%"
            - "   §*&4* &f暴击伤害 &f+&c(30-150)%"
            - " "
    #启动制作动作(设置 cancel 则取消制作)
    #该位置触发的时候就已经可以显示获取到材料数据
    start-actions:
      1:
        - condition:
            #判断物品是否不可重铸
            - "check '{material-data *勇士之剑 *lore-contains *不可重铸}' == true"
          meet:
            - "send '&f你放入的 &6勇士之剑 &f物品被系统限制为不可重铸物品'"
            - "cancel_all"
      2:
        - condition:
            #判断放入的重铸石数量
            #因为上方 materials 配置内的重铸石没有写数量限制,可在这里写
            - "check '{material-data *重铸石 *get-amount}' <= 10"
          not-meet:
            - "send '&f你放入的 &6重铸石 &f数量过多,请减少至 &c10 &f颗或以下'"
            - "cancel_all"
      3:
        - meet:
            #设置默认重铸概率
            - "craft:data *重铸概率 *add *20.0"
            #读取所有放入的材料上 "+(.*?)% 重铸概率" 上的概率值 (该读取最终还会乘以放入的材料数量)
            - "craft:data *重铸概率 *add *{material-central *lore-value *+(.*?)% 重铸概率}"
            - "craft:data *重铸强度 *add *{material-central *lore-value *+(.*?)% 重铸强度}"
    actions:
      #主动作组
      1:
        #子动作组
        1:
          - condition:
              #模拟重铸概率,并判断是否放入的保护符
              - "check random 100 <= {data *重铸概率 *50.0}"
            meet:
              #重铸概率判断通过,取消该主动作组内所有子动作组运行
              #这里的 cancel_sub 跟 cancel_all 区别在于 cancel_sub 只作用于子动作组内,而 cancel_all为所有动作组
              - "cancel_sub"
            not-meet:
              #发送消息
              - "send '&f你在重铸 &6勇士之剑 &f时发生炸炉,毁于一旦 ({data *重铸概率 *50.0})'"
        2:
          - condition:
              #判断是否放入的保护符
              - "check '{material-central *key-contains *重铸保护符}' == true"
            meet:
              - "send '&f你在重铸时放入了保护符 &a装备未损毁'"
              #将重铸的物品原封不动的复制回去
              - "craft:describe *copy-material *勇士之剑"
              #结束制作并提取物品
              - "craft:system *extract-stop"
              #取消接下来的所有动作组运行
              - "cancel_all"
            not-meet:
              - "send '&f你在重铸时未放入保护符 &c装备损毁了'"
              #结束制作(物品损毁,因为没放入保护符道具)
              - "craft:system *stop"
              #取消接下来的所有动作组运行
              - "cancel_all"
      2:
        1:
          - meet:
              #使用 copy-material 复制放入材料位上的 勇士之剑 物品数据
              #该方法会复制物品数据上的 类型、数量、名称、描述 等数据
              - "craft:describe *copy-material *勇士之剑"
              #使用 replace-group 将包含指定字符的LORE替换为 描述组 内的内容
              - "craft:describe *replace-group *§*§f* *物理属性重铸"
              - "craft:describe *replace-group *§*§c* *暴击几率重铸"
              - "craft:describe *replace-group *§*§4* *暴击伤害重铸"

material-displays:
  "勇士之剑":
    material: BARRIER
    name: "§6勇士之剑 §f(1)"
    lore:
      - " "
      - "  §f请放入 §6勇士之剑 §f武器"
      - "  §f该物品需为 §6可重铸 §f状态"
      - " "
  "重铸石":
    material: BARRIER
    name: "§6重铸石 §f(1-10)"
    lore:
      - " "
      - "  §f重铸任意装备必须材料"
      - "  §f该处理可开启 §6重铸宝箱 §f获得"
      - " "
  "重铸保护符":
    material: BARRIER
    name: "§6重铸保护符 §f(1)"
    lore:
      - " "
      - "  §f重铸任意装备时放入改道具"
      - "  §f可防止重铸装备 §c损毁"
      - " "
```
