# 体力系统的宝箱示例

## 例子配置

自带体力系统的宝箱示例，机制基本上都可以自定义，可以配合其他体力插件的变量

```yaml
#这个宝箱带有体力系统,当体力为 0 时无法开启该类型的宝箱
#体力每一分钟恢复 1 点,上限 10 点

content-name: "简单的例子(体力宝箱)"
#将 data object 对象数据储存至数据库
content-object-store: true
#将 data content 工作组数据储存至数据库
content-store: true

basic-entity:
  - entity-collision-size: 1
    entity-type: "SLIME"
    default-name: 宝箱
basic-block:
  - default-skull-name: model:grass
    type: CREEPER_HEAD
    default-name: 宝箱

generate-action:
  #设置所有玩家默认体力值为 10 点
  0:
    - condition:
        - check '${job:content *data *%player_name%的体力值 *int *-1}' == -1
      condition-is-met:
        - job:data content set %player_name%的体力值 10
  1:
    - condition:
        #判断当前时间戳是否大于玩家数据储存的时间戳,大于则宝箱显示可开启,小于则宝箱隐藏不可开启
        - check '${job:time *current}' >= '${job:player *data *宝箱开启冷却时间戳 *int}'
      condition-is-met:
        #上方判断满足,设置为显示状态,玩家可以看到该宝箱
        - job:visible self object true
        - job:hologram send self 宝箱全息
      condition-not-met:
        #上方判断不满足,设置为隐藏状态,玩家不可看到该宝箱
        - job:visible self object false

action-steps:
  宝箱:
    1:
      - condition:
          - check '${job:content *data *%player_name%的体力值 *int *0}' <= 0
        condition-is-met:
          - send "&f你的体力值无法开启该宝箱"
          #终止接下来的脚本运行
          - job:script stop
    2:
      - condition-is-met:
          - send "&f你开启了一个 &6宝箱 &f消耗 &c1 &f点体力,当前剩余 §6${job:content *data *%player_name%的体力值 *int *0}/10"
          - job:visible self object false
          #扣除 1 点体力值
          - job:data content take %player_name%的体力值 1
          - job:data player set 宝箱开启冷却时间戳 ${job:time *current *10}

          #掉落物品(模拟开宝箱奖励)
          - job:item drop o DIAMOND 1 #掉一个钻石
          - job:item drop o DIAMOND 3 ~@0.5 #50%概率多掉三个钻石
          - job:item drop o DIAMOND_SWORD 1 ~@0.1 #10%概率掉一把钻石剑
    type:
      - LEFT_CLICK

tasks:
  #每 60 秒恢复所有玩家 1 点体力值
  "体力系统-自动启动":
    type: "CONTENT"
    run-type: "CYCLE"
    run-time: 60
    run-auto: true
    #所有对象数据 (默认开启状态)
    #开启后任务触发会根据服务器内所属该对象数量,全部触发一遍
    #开启后可使用 object 对象相关的脚本
    object-data: false
    online-player-run: true
    action-steps:
      1:
        - condition:
            - check '${job:content *data *%player_name%的体力值 *int *0}' < 10
          condition-is-met:
            - job:data content add %player_name%的体力值 1

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
            - job:visible self object true
            - job:hologram send self 宝箱全息

hologram:
  high: 2.2
  update: true
  "宝箱全息":
    - "§f[ §6§l宝箱§f ]"
    - "§f宝箱状态: §a可开启"
    - "§f玩家体力 §6${job:content *data *%player_name%的体力值 *int *0} / 10 §c(-1)"
```
