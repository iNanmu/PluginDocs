# 循环的宝箱示例

## 例子配置

```yaml
#这个宝箱生成后,每个玩家每十秒可开启一次该宝箱
#可以自定义开启间隔时间,具体自己看看下面的配置内容

#游戏内输入 /frame create 简单的例子(宝箱2) ENTITY true 即可生成对象
content-name: "简单的例子(宝箱2)"

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
        #判断当前时间戳是否大于玩家数据储存的时间戳,大于则宝箱显示可开启,小于则宝箱隐藏不可开启
        - check '${job:time *current}' >= '${job:player *data *宝箱开启冷却时间戳 *int}'
      condition-is-met:
        #上方判断满足,设置为显示状态,玩家可以看到该宝箱
        - job:visible self object true
      condition-not-met:
        #上方判断不满足,设置为隐藏状态,玩家不可看到该宝箱
        - job:visible self object false

action-steps:
  宝箱:
    1:
      - condition-is-met:
          - send "&f你开启了一个 &6宝箱"
          #隐藏玩家对该宝箱的可视度
          - job:visible self object false
          #设置玩家宝箱冷却时间 (记录冷却完成的时间戳)
          #${job:time *current *10} = 获取十秒后的时间戳
          - job:data player set 宝箱开启冷却时间戳 ${job:time *current *10}

          #掉落物品(模拟开宝箱奖励)
          - job:item drop o DIAMOND 1 #掉一个钻石
          - job:item drop o DIAMOND 3 ~@0.5 #50%概率多掉三个钻石
          - job:item drop o DIAMOND_SWORD 1 ~@0.1 #10%概率掉一把钻石剑
    type:
      - LEFT_CLICK

#任务详细介绍可以查看WIKI
tasks:
  "宝箱开启冷却任务-自动启动":
    type: "CONTENT"
    run-type: "CYCLE"
    run-time: 1
    run-auto: true
    online-player-run: true
    action-steps:
      1:
        - condition:
            - check '${job:player *visible *object}' == false
            - check '${job:time *current}' >= '${job:player *data *宝箱开启冷却时间戳 *int}'
          condition-is-met:
            #上方条件满足后,将玩家对该宝箱的可视度设为显示
            - job:visible self object true


#全息详细介绍可以查看WIKI
hologram:
  high: 1.8
  update: true
  default:
    "宝箱":
      - "§f[ §a右键开启宝箱 §f]"
      - "§f每个玩家每十秒有一次机会开启该宝箱"
```
