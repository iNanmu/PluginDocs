# 强化示例

## MythicMobs 物品配置

你可以使用一下物品配置，配合该示例功能在游戏内亲身使用一次该功能，那能让你更好的理解改示例

可在游戏内通过 `/craft make 你的名字 武器强化` 打开强化界面

```yaml
普通的铁剑:
  Id: IRON_SWORD
  Display: '&6普通的铁剑'
  Lore:
  - '&f装备类型: 武器'
  - ' '
  - '&6基础属性'
  - '&f物理伤害 &c+30'
  - '&f暴击几率 &c+5'
  - '&f暴击伤害 &c+30'
  - ' '
  - '&a可强化'
  
强化石:
  Id: COAL
  Display: '&6强化石'
  Lore:
  - ' '
  - '&6&l* &7材料介绍'
  - '   &f* &7强化任意装备必须材料'
  - '   &f* &7该处理可开启 &6强化宝箱 &7获得'
  - ' '
  - '&6&l* &7材料加成'
  - '   &f* &f+10% 强化成功率'
  - ' '
```

## 强化示例

```yaml
content-name: "武器强化"
class: "强化类目"
interface: "强化界面"
#默认学会该图纸
default-learn: true
#提取物品后返回工艺制作界面
extract-return: true

phases:
  1:
    time: 0
    materials:
      1:
        #放入的材料必须包含能匹配上的 "装备类型: 武器" 描述(LORE)
        lore: "§f装备类型: 武器"
        must: true
        amount: 1
        display: "强化物"
        data: "强化物"
      2:
        name: "强化石"
        must: true
        display: "强化石"
        data: "强化石"
      3:
        name: "保护符"
        must: false
        amount: 1
        display: "保护符"
        data: "保护符"
    introduce:
      material: IRON_SWORD
      name: "§f强化物品属性"
      lore-displays:
        1:
          lore:
            - " "
            - "&f▪ &f强化成功概率 &c50 &f%"
            - "&f▪ &f可强化物品类型 &6武器"
            - " "
            - "&f▪ &f强化成功后将对物品 &6基础属性 &f进"
            - "&f▪ &f行属性强化, 最高强化值 &c+15 &f级,当"
            - "&f▪ &f装备强化 &c+10 &f以上失败时有 &c30%"
            - "&f▪ &f概率武器破损"
            - " "
            - "&f▪ &a强化成功 &f将提高 &c8% &f基础属性值"
            - "&f▪ &c强化失败 &f将降低 &c8% &f基础属性值"
    start-actions:
      1:
        - condition:
            #判断放入的 强化物 是否小于 15 级
            - "check '{material-data *强化物 *get-nbt *强化等级NBT *0}' < 15"
          meet:
            - "craft:data *强化等级 *set *{material-data *强化物 *get-nbt *强化等级NBT *0}"
          not-meet:
            - "send '&f你放入的强化物品已 +15 无法继续强化'"
            - "cancel_all"
      2:
        - condition:
            - "check '$[1+({data *强化等级 *0}*2)]' > '{material-data *强化石 *get-amount}'"
          meet:
            - "send '&f强化 &c+{data *强化等级 *0} &f的装备,你需要放入 &c$[1+({data *强化等级 *0}*2)] &f颗强化石'"
            - "cancel_all"
      3:
        - meet:
            #设置默认重铸概率
            - "craft:data *成功概率 *add *50.0"
            #读取所有放入的材料上 "+(.*?)% 强化成功率" 上的概率值 (该读取最终还会乘以放入的材料数量)
            - "craft:data *成功概率 *add *{material-central *lore-value *+(.*?)% 强化成功率}"
      4:
        - condition:
            #判断是否放入了保护符材料
            - "check '{material-central *data-contains *key-contains *保护符}' == true"
          meet:
            #设置保护符放入状态为 true 下面有判断要用到
            - "craft:data *是否放入保护符 *set *true"
    actions:
      1:
        1:
          - meet:
              #复制强化物上的所有数据
              - "craft:describe *copy-material *强化物"
        2:
          - condition:
              #判断是否已经储存过物品原始名
              - "check '{material-data *强化物 *get-nbt *强化物品原名NBT *null}' == 'null'"
            meet:
              #未储存过物品原始名时触发
              #储存物品未升级时的物品名字,后面要把卡牌改成 卡牌名 +1、+2、+3... 的格式
              - "craft:nbt *set *强化物品原名NBT *string *{material-data *强化物 *get-name}"
              - "craft:data *强化物品原名 *set *{material-data *强化物 *get-name}"
            not-meet:
              #储存过物品原始名时触发
              - "craft:data *强化物品原名 *set *{material-data *强化物 *get-nbt *强化物品原名NBT}"
      2:
        1:
          - condition:
              #强化等级小于三级时强化必定成功
              - "any [ check random 100 <= '{data *成功概率 *50}' check '{data *强化等级 *0}' < 3 ]"
            meet:
              #强化成功,强化等级+1
              - "craft:data *强化等级 *set *$[{data *强化等级 *0}+1]"
              #触发自定义动作组,增强强化物属性
              - "craft:system *perform-actions *强化属性提升 *1"
              #发送消息
              - "send '&f强化成功,当前物品强化等级 &c+{data *强化等级 *0}'"
              #取消接下来的动作运行
              - "cancel_sub"
        2:
          - condition:
              #强化失败,当强化等级大于10级有30%概率导致装备破损,如果放入了保护符则一定不破损
              - "all [ check '{data *强化等级 *0}' > 10 check random 100 >= 30 check '{data *是否放入保护符 *false}' == false ]"
            meet:
              - "send '&c强化失败,装备承受不住破损了"
              - "craft:system *stop"
              - "cancel_all"
        3:
          - meet:
              #强化失败扣除强化等级
              - "craft:data *强化等级 *set *$[{data *强化等级 *0}-1]"
              #触发自定义动作组,降低强化物属性
              - "craft:system *perform-actions *强化属性降低 *1"
              #发送消息
              - "send '&f强化失败,当前物品强化等级 &c+{data *强化等级 *0}'"

    #提取物品时触发动作
    extract-actions:
      0:
        - meet:
            #储存强化等级至NBT
            - "craft:nbt *set *强化等级NBT *int *{data *强化等级 *0}"
            #修改物品名
            - "craft:name *{data *强化物品原名} §f+{data *强化等级 *0}"

custom-actions:
  "强化属性提升":
    1:
      1:
        - meet:
            #获取描述 §6基础属性 至 空白行 之间的描述并进行公式计算并替换
            - "craft:describe *replace-part-value *§6基础属性 *  *@value+(@value*8.0/100) *true"
  "强化属性降低":
    1:
      1:
        - meet:
            #获取描述 §6基础属性 至 空白行 之间的描述并进行公式计算并替换
            - "craft:describe *replace-part-value *§6基础属性 *  *@value-(@value*8.0/100) *true"

material-displays:
  "强化物":
    material: BARRIER
    name: "§f强化物 (&6武器&f)"
    lore:
      - " "
      - "&f▪ &f请放入装备类型为 &6武器 &f的装备"
      - "&f▪ &f进行强化"
      - " "
  "强化石":
    material: BARRIER
    name: "§6强化石"
    lore:
      - " "
      - "&f▪ &f请放入 &6强化石 &f强化石数量要求"
      - "&f▪ &f为 &c1+(装备强化等级*2) &f颗"
      - " "
  "保护符":
    material: BARRIER
    name: "§6保护符"
    lore:
      - " "
      - "&f▪ &f强化 &c+10 &f以上装备时可防止装备"
      - "&f▪ &f破损"
      - " "
```
