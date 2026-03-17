# 炼药示例

## MythicMobs 物品配置

你可以使用一下物品配置，配合该示例功能在游戏内亲身使用一次该功能，那能让你更好的理解改示例

可在游戏内通过 `/craft make 你的名字 三清` 打开炼制三清丹药界面

```yaml
一清草:
  Id: WHEAT
  Display: '&3一清草'
  Lore:
  - ' '
  - '&6&l* &7草药介绍'
  - '   &f* &7炼制 &6三清丹 &7必须材料'
  - '   &f* &7可开启 &6草药宝箱 &7获得'
  - ' '
  - '&6&l* &7额外药性'
  - '   &f* &f生命力 &f+&c100 &f(一清草)'
  
二清草:
  Id: WHEAT
  Display: '&3二清草'
  Lore:
  - ' '
  - '&6&l* &7草药介绍'
  - '   &f* &7炼制 &6三清丹 &7必须材料'
  - '   &f* &7可开启 &6草药宝箱 &7获得'
  - ' '
  - '&6&l* &7额外药性'
  - '   &f* &f移动速度 &f+&c10&f% &f(二清草)'
  
三清草:
  Id: WHEAT
  Display: '&3三清草'
  Lore:
  - ' '
  - '&6&l* &7草药介绍'
  - '   &f* &7炼制 &6三清丹 &7必须材料'
  - '   &f* &7可开启 &6草药宝箱 &7获得'
  - ' '
  - '&6&l* &7额外药性'
  - '   &f* &f物理伤害 &f+&c5&f(%) &f(三清草)'
```

## 炼药示例

```yaml
content-name: "三清"
class: "炼药类目"
interface: "炼药界面"

quality:
  "上品": 10.0
  "中品": 50.0
  "下品": 100.0

describes:
  "丹药基础内容":
    - " "
    - "&6&l† &7丹药信息"
    - "   &f▪ &f右键使用将在 &c{random *r:10-100 *1.0} &f秒"
    - "   &f▪ &f内获得丹药属性加成"
    - " "
    - "&6&l† &7丹药药性"
    - "   &f▪ &f生命力 &f+&c{random *r:100-1000 *0.1}"
    - "   &f▪ &f物理伤害 &f+&c{random *r:10-100 *0.1}"
    - " "

phases:
  1:
    time: 10
    extract: true
    materials:
      1:
        name: "§3一清草"
        must: true
        amount: 1
        display: "一清草"
        data: "一清草"
      2:
        name: "§3二清草"
        must: true
        amount: 1
        display: "二清草"
        data: "二清草"
      3:
        name: "§3三清草"
        must: true
        amount: 1
        display: "三清草"
        data: "三清草"
    introduce:
      material: SLIME_BALL
      name: "§6三清丹"
      lore-displays:
        1:
          lore:
            - " "
            - "&f▪ &f成丹概率 &c50 &f%"
            - " "
            - "&6&l† &7丹药信息"
            - "   &f▪ &f右键使用将在 &c(1-100) &f秒"
            - "   &f▪ &f内获得丹药属性加成"
            - " "
            - "&6&l† &7丹药药性"
            - "   &f▪ &f生命力 &f+&c(100-1000)"
            - "   &f▪ &f物理伤害 &f+&c(10-100)"
            - " "
    #启动制作动作(设置 cancel 则取消制作)
    #该位置触发的时候就已经可以显示获取到材料数据
    start-actions:
      1:
        - meet:
            #设置默认成丹概率
            - "craft:data *成丹概率 *add *50.0"
            #读取所有放入的材料上 "+(.*?)% 成丹概率" 上的概率值
            - "craft:data *成丹概率 *add *{material-central *lore-value *+(.*?)% 成丹概率}"
    actions:
      #主动作组
      1:
        #子动作组
        1:
          - condition:
              #模拟炼丹成功概率
              - "check random 100 <= {data *成丹概率 *50.0}"
            not-meet:
              #结束制作
              - "craft:system *stop"
              #发送消息
              - "send '&f你在炼制 &6三清纹 &f发生炸炉,毁于一旦 ({data *成丹概率 *50.0})'"
              #发送爆炸效果 (安装Chemdah的用户可以模拟炸炉爆炸效果,没有的自己配置个Command吧)
              #- "particle normal 'hugeexplosion 0 0 0 -count 10 -speed 0.1' at location @self"
              #取消接下来所有动作组的运行
              - "cancel_all"
        2:
          - meet:
              #设置制作物类型
              - "craft:type *SLIME_BALL"
              #设置炼制物名称
              - "craft:name *§6三清纹"
              #为炼制物加上丹药基础属性描述内容
              - "craft:describe *add *丹药基础内容"
              #增加熟练度
              - "craft:system *proficiency *add *{random *r:10-50}"
        3:
          - condition:
              #判断工艺熟练度大于 50 时,可炼制出 1~2 颗丹药
              - "check '{content *proficiency}' >= 50.0"
            meet:
              #设置数量(默认1)
              - "craft:amount *{random *r:1-2}"
        4:
          - condition:
              #判断工艺熟练度大于 100 时,可炼制出 2~5 颗丹药
              - "check '{content *proficiency}' >= 100.0"
            meet:
              - "craft:amount *{random *r:2-5}"
      2:
        1:
          - condition:
              #检测放入的三样炼制材料是否存在额外药性加成的描述
              - "any [ check '{material-central *lore-filter-size *§f(一清草),§f(二清草),§f(三清草)}' > 0 ]"
            meet:
              #满足上方条件为炼制的丹药加上描述
              - "craft:describe *add-line *&6&l† &7额外药性"
              #使用 material-central 占位符,读取对应炼制材料描述内符合条件的LORE,增加至炼制的丹药上
              - "craft:describe *add-line *{material-central *plugin-lore-filter *§f(一清草),§f(二清草),§f(三清草)}"
              #下方脚本行可简写成上方这行脚本
              #- "craft:describe *add-line *{material-data *一清草 *plugin-lore-filter *§f(一清草)}"
              #- "craft:describe *add-line *{material-data *二清草 *plugin-lore-filter *§f(二清草)}"
              #- "craft:describe *add-line *{material-data *三清草 *plugin-lore-filter *§f(三清草)}"

material-displays:
  "一清草":
    material: BARRIER
    name: "§3一清草 §cx §f1"
    lore:
      - " "
      - "  §f炼制三清纹丹药必须草药"
      - "  §f该草药可开启 §6草药宝箱 §f获得"
      - " "
  "二清草":
    material: BARRIER
    name: "§3二清草 §cx §f1"
    lore:
      - " "
      - "  §f炼制三清纹丹药必须草药"
      - "  §f该草药可开启 §6草药宝箱 §f获得"
      - " "
  "三清草":
    material: BARRIER
    name: "§3三清草 §cx §f1"
    lore:
      - " "
      - "  §f炼制三清纹丹药必须草药"
      - "  §f该草药可开启 §6草药宝箱 §f获得"
      - " "
```
