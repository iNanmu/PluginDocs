# 蓝水晶矿示例 (过时)

## 介绍

生成蓝水晶矿的一个对象，这个例子内包含 **矿物生长、矿物开采冷却、矿物开采进度** 当 **开采进度 < 80 每次开采则获得蓝水晶碎片** 当 **开采进度 >=80 则获得蓝水晶之心** 并重新进入 **矿物生长周期** 该例子内的 **对象数据(冷却、开采进度)是全服玩家共享** 但 **不同对象之间数据互不干扰**

## 演示

哔哩哔哩: [https://www.bilibili.com/video/BV1NA4y197Yt/](https://www.bilibili.com/video/BV1NA4y197Yt/)

演示视频内的 **模型，配置** 均可在售后群文件内获取

## 配置

```yaml
content-name: "蓝水晶矿"

#如果对象需要 跨服数据实时互通(MySQL) 或 保存相关数据以备下次服务器重启 进行读取
#工作组所属对象数据实时储存至数据库或本地数据库
content-object-store: false
#工作组数据实时储存至数据库或本地数据库
content-store: false

#方块对象设置 (因为这个例子是以实体对象为主设计的,所以可有可无)
basic-block:
    #方块类型
  - type: CREEPER_HEAD
    default-name: "蓝水晶矿根"
    #头颅数据 (可配合萌芽方块,龙之方块)
    default-skull-name: "model:grass"
#实体对象设置
basic-entity:
    #史莱姆实体碰撞箱大小 (仅为史莱姆时可使用)
  - entity-collision-size: 1
    #实体类型
    entity-type: "SLIME"
    #默认实体对象显示名(可配合萌芽、龙核实体模型)
    default-name: "蓝水晶矿根"

#玩家首次加载对象时触发,每次进服的时候也会触发
generate-action:
  #这个主要是防止玩家重新进服后不显示蓝水晶矿还是显示蓝水晶矿根 (生长时间已经为 0 的时候)
  0:
    - condition:
        #检测生长时间是否为 0 秒
        - check "${job:object *data *growth_time}" == 0
      condition-is-met:
        - job:object name self 蓝水晶矿


#对象第一次加载到服务器上时触发脚本动作处理 (无玩家)
init-action:
  0:
    - condition-is-met:
        #设置生长时长 growth_time 为 10
        - job:data object set growth_time 10
        #启动 蓝水晶生长周期 任务
        - job:task perform object 蓝水晶生长周期

action-steps:
  #因为上方设置 default-name 为 蓝水晶矿根 所以最开始一定会触发这段动作内的步骤
  "蓝水晶矿根":
    type:
      - RIGHT_CLICK
      - LEFT_CLICK
    1:
      - condition-is-met:
          - send *"§f[§6§l!§f] §b蓝水晶 §f还生成还有 §c${job:object *data *growth_time} §f秒"
  #当蓝水晶生长周期任务执行完毕,对象名会被修改为 蓝水晶矿 从而开始执行这段动作内的步骤
  "蓝水晶矿":
    type:
      - LEFT_CLICK
    #判断玩家背包上方存在相对应的物品
    1:
      - condition:
          - check "${job:player *check-hand *main *§b她家的稿 *1 *false}" == "true"
        condition-not-met:
          - send "§f[§6§l!§f] §f你需要手持 §b她家的稿 §f才内采集这个款物"
          #如果没有这个物品的话就停止接下来 2、3 号步骤的处理
          - job:script stop
    #判断对象是否存在冷却
    2:
      - condition:
          - check "${job:object *data *cooling}" >= 1
        condition-is-met:
          - send "§f[§6§l!§f] §f该 §6蓝水晶 §f刚被开采过,请等待 §c${job:object *data *cooling} §f秒后再来"
          #在冷却的话就停止接下来 3 号步骤的处理
          - job:script stop
    #执行矿物采集内容
    #因为是测试示例我这里面没有写实际给玩家物品的脚本,只写了提醒
    3:
      #判断采集进度是否大于等于 80
      - condition:
          - check "${job:object *data *mining_degree}" >= 80
        #大于等于 80 就执行这里面的脚本内容
        condition-is-met:
          - send "§f[§6§l!§f] §6蓝水晶 §f开采完毕,获得 §6蓝水晶之心x1"
          - job:particle all STAR CLOUD 3
          #发送矿物被挖掉的动作
          - job:germ animation start all death
          #启动 蓝水晶开采完毕 任务
          - job:task perform object 蓝水晶开采完毕
        #小于 80 就执行这里面的脚本内容
        condition-not-met:
          #设置 cooling 冷却为 3
          - job:data object set cooling 3
          #增加该对象的开采进度 mining_degree + 20
          - job:data object add mining_degree 20
          #发送粒子特效
          - job:particle all SPHERE CLOUD 4
          - send "§f[§6§l!§f] §f成功开采 §6蓝水晶 §f获得 §6蓝水晶碎片x1"
          - send "§f[§6§l!§f] §f该 §6蓝水晶 §f的开采度为 ${job:object *data *mining_degree}"

tasks:
  #插件加载这个工作组的时候就开始运行 (不用在对象动作处理步骤内启动)
  "蓝水晶冷却":
    type: "CONTENT"
    run-type: "CYCLE"
    run-time: 1
    run-auto: true
    action-steps:
      1:
        - condition:
            #判断当对象数据 cooling 内的值是否大于等于 1
            - check "${job:object *data *cooling}" >= 1
          condition-is-met:
            #大于等于 1 的话每次减 1 (这里相当于每秒减 1 冷却)
            - job:data object take cooling 1

  #这个任务主要是防止我在动作处理步骤内的 death 动作还没触发完就被改模型
  "蓝水晶开采完毕":
    type: "OBJECT"
    run-type: "DELAY"
    run-time: 2
    action-steps:
      1:
        - condition-is-met:
            #将矿物挖掉后重新将对象名修改为 蓝水晶矿根
            - job:object name all 蓝水晶矿根
            #清除原先该对象数据内的 mining_degree (开采进度)
            - job:data object remove mining_degree
            #设置生长时长 growth_time 为 10
            - job:data object set growth_time 10
            #再次启动 蓝水晶生长周期 任务
            - job:task perform object 蓝水晶生长周期

  #生成蓝水晶矿任务 (蓝水晶矿根 -> 蓝水晶矿)
  "蓝水晶生长周期":
    type: "OBJECT"
    run-type: "CYCLE"
    run-time: 1
    action-steps:
      1:
        - condition:
            #判断生长所需时长是否大于等于 1
            - check "${job:object *data *growth_time}" >= 1
          condition-is-met:
            #大于等于 1 的话就减 1
            - job:data object take growth_time 1
          condition-not-met:
            #当生长所需时长小于 1 时触发这里面的内容 (开始生成为 蓝水晶矿)
            - job:object name all 蓝水晶矿
            - job:particle all STAR CLOUD 3
            - job:particle all SPHERE CLOUD 5
            #停止 蓝水晶生长周期 任务继续运行
            - job:task cancel object 蓝水晶生长周期
      2:
        - condition:
            #判断生长所需时长是否等于 3
            - check "${job:object *data *growth_time}" == 3
          condition-is-met:
            #等于 3 的话就运行萌芽模型动作 (这个你就自己把握好生成动画的时长吧)
            - job:germ animation start all generate
```
