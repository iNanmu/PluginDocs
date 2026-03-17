# 草药采集示例

```yaml
#游戏内输入 /frame create 简单的例子(草药采集) ENTITY true 即可生成对象
content-name: "简单的例子(草药采集)"

#这部分基础的内容,你可以看看WIKI
basic-entity:
  - entity-collision-size: 1
    entity-type: "SLIME"
    default-name: 草药
basic-block:
  - default-skull-name: model:grass
    type: CREEPER_HEAD
    default-name: 草药

persistent-steps:
  #模拟采集草药的等待效果
  "草药采集":
    #开始采集时提醒
    start:
      1:
        - condition-is-met:
            - send *"&f开始采摘 &6草药"
    #按秒依次运行
    timing:
      1:
        1:
          - condition-is-met:
              - title "§6采集草药" subtitle "§a|||||§c|||||||||||||||" by 0 60 0
              - sound AMBIENT_CAVE
      3:
        1:
          - condition-is-met:
              - title "§6采集草药" subtitle "§a|||||||§c|||||||||||||" by 0 60 0
              - sound AMBIENT_CAVE
      5:
        1:
          - condition-is-met:
              - title "§6采集草药" subtitle "§a||||||||||||§c||||||||" by 0 60 0
              - sound AMBIENT_CAVE
      7:
        1:
          - condition-is-met:
              - title "§6采集草药" subtitle "§a|||||||||||||||||§c|||" by 0 60 0
              - sound AMBIENT_CAVE
      9:
        1:
          - condition-is-met:
              - title "§6采集草药" subtitle "§a||||||||||||||||||||" by 0 60 0
              - sound AMBIENT_CAVE
      10:
        1:
          - condition-is-met:
              #持续交互动作完毕后发生草药采集奖励
              #这里的 草药采集奖励 是下面 action-steps 配置预设项
              - job:step cast 草药采集奖励
              #终止持续交互组
              - job:persistent stop 草药采集

action-steps:
  草药:
    1:
      - condition-is-met:
          #启动持续交互组 草药采集 是上面 persistent-steps 配置预设项
          - job:persistent start 草药采集
    type:
      - LEFT_CLICK

  草药采集奖励:
    1:
      - condition-is-met:
          #触发命令
          - command "say 100% 触发的命令" as op
          #触发命令后面加了 ~@0.5 代表 50% 概率触发
          #注意概率触发格式适用于所有脚本行,不仅限于 command 脚本
          - command "say 50% 触发的命令" as op ~@0.5
          - command "say 10% 触发的命令" as op ~@0.1

#全息详细介绍可以查看WIKI
hologram:
  high: 1.8
  update: true
  default:
    #全息
    "草药":
      - "§f[ §a可采集 §f]"
```
