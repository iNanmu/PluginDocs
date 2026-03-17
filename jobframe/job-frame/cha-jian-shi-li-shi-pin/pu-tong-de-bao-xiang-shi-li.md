# 普通的宝箱示例

## 例子配置

```yaml
#这个宝箱生成后,每个玩家只能开启一次(注意是每个玩家)

#游戏内输入 /frame create 简单的例子(宝箱1) ENTITY true 即可生成对象
content-name: "简单的例子(宝箱1)"
#往下看有介绍作用,这个是将 object 设置的数据储存至数据库
content-object-store: true

#这部分基础的内容,你可以看看WIKI
basic-entity:
  - entity-collision-size: 1
    entity-type: "SLIME"
    default-name: 宝箱
basic-block:
  - default-skull-name: model:grass
    type: CREEPER_HEAD
    default-name: 宝箱

#玩家进服时会触发
generate-action:
  0:
    - condition:
        #判断玩家是否已经开启过该宝箱,默认 false 为未开过
        - check "${job:object *data *%player_name%宝箱开启状态 *str *false}" == true
      condition-is-met:
        #如果已开启过宝箱则隐藏改对象,开启过的玩家将看不到该宝箱
        - job:visible self object false

action-steps:
  宝箱:
    1:
      - condition-is-met:
          - send "&f你开启了一个 &6宝箱"
          #隐藏玩家对该宝箱的可视度
          - job:visible self object false
          #设置玩家对该宝箱的开启状态为 true
          #注意只有 "content-object-store: true" 状态下,该开启状态数据才会储存至数据库
          #如果为 false 的话,该状态服务器重启后即刻重置,玩家就又可以开启一次该宝箱了
          - job:data object set %player_name%宝箱开启状态 true

          #掉落物品(模拟开宝箱奖励)
          - job:item drop o DIAMOND 1 #掉一个钻石
          - job:item drop o DIAMOND 3 ~@0.5 #50%概率多掉三个钻石
          - job:item drop o DIAMOND_SWORD 1 ~@0.1 #10%概率掉一把钻石剑
    type:
      - LEFT_CLICK

#全息详细介绍可以查看WIKI
hologram:
  high: 1.8
  default:
    "宝箱":
      - "§f[ §a右键开启宝箱 §f]"
      - "§f每个玩家仅有一次机会开启该宝箱"
```
