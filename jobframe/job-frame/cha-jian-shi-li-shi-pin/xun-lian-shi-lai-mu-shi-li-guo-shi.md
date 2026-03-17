# 训练史莱姆示例 (过时)

## 演示

哔哩哔哩:[ ](https://www.bilibili.com/video/BV1bA4y197yb/)[https://www.bilibili.com/video/BV1bA4y197yb/](https://www.bilibili.com/video/BV1bA4y197yb/)

演示视频内的 **模型，配置** 均可在售后群文件内获取

## 配置

```yaml
content-name: "训练史莱姆"
content-object-store: true

basic-block:
  - type: CREEPER_HEAD
    default-name: "史莱姆训练地"
    default-skull-name: "model:grass"
basic-entity:
  - entity-collision-size: 1
    entity-type: "SLIME"
    default-name: "史莱姆训练地"

generate-action:
  0:
    - condition:
        - check "${job:object *data *所转职业}" == "剑士"
      condition-is-met:
        - job:object name self §6史莱姆剑士
        - job:script stop
  1:
    - condition:
        - check "${job:object *data *所转职业}" == "法师"
      condition-is-met:
        - job:object name self §b史莱姆法师
        - job:script stop
  2:
    - condition:
        - check "${job:object *data *正在训练的玩家}" != "0"
      condition-is-met:
        - job:object name self 史莱姆小兵

action-steps:
  "史莱姆训练地":
    type:
      - RIGHT_CLICK
    1:
      - condition:
          - all [ check "${job:object *data *正在训练的玩家}" != "%player_name%" check "${job:object *data *正在训练的玩家}" != "0" ]
        condition-is-met:
          - send "§f[§6§l!§f] §f这个训练场地已经被 ${job:object *data *正在训练的玩家} 玩家占领"
          - job:script stop
    2:
      - condition:
          - all [ check "${job:player *check-hand *main *§a普通史莱姆 *1 *true}" == "true" check "${job:object *data *正在训练的玩家}" == "0" ]
        condition-not-met:
          - send "§f[§6§l!§f] §f请手持一只 §a普通史莱姆"
          - job:script stop
    3:
      - condition-is-met:
          - send "§f[§6§l!§f] §f成功占领当前训练地!"
          - job:data object set 还需训练时长/秒 10
          - job:data object set 正在训练的玩家 %player_name%
          - job:object name all 史莱姆小兵
          - job:script stop


  "史莱姆小兵":
    type:
      - RIGHT_CLICK
    1:
      - condition:
          - all [ check "${job:object *data *正在训练的玩家}" != "%player_name%" check "${job:object *data *正在训练的玩家}" != "0" ]
        condition-is-met:
          - send "§f[§6§l!§f] §f${job:object *data *正在训练的玩家} 正在这里训练他的史莱姆"
          - job:script stop
    2:
      - condition:
          - check "${job:object *data *还需训练时长/秒}" > 0
        condition-is-met:
          - send "§f[§6§l!§f] §f你的史莱姆训练时长还不够,再训练 ${job:object *data *还需训练时长/秒} 秒再来吧"
          - job:script stop
    3:
      - condition:
          - all [ check "${job:player *check-hand *main *§6木剑 *1 *false}" == "false" check "${job:player *check-hand *main *§b法杖 *1 *false}" == "false" ]
        condition-is-met:
          - send "§f[§6§l!§f] §f史莱姆可以选择转职业了!"
          - send "§f[§6§l!§f] §f给史莱姆 §6木剑 §f可以转职为史莱姆剑士"
          - send "§f[§6§l!§f] §f给史莱姆 §b法杖 §f可以转职为史莱姆法师"
          - job:script stop
    4:
      - condition:
          - check "${job:player *check-hand *main *§6木剑 *1 *true}" == "true"
        condition-is-met:
          - send "§f[§6§l!§f] §f史莱姆成功转职为 §6史莱姆剑士"
          - job:data object set 还需训练时长/秒 10
          - job:data object set 所转职业 剑士
          - job:entity collision all 2
          - job:object name self §6史莱姆剑士
          - job:script stop
    5:
      - condition:
          - check "${job:player *check-hand *main *§b法杖 *1 *true}" == "true"
        condition-is-met:
          - send "§f[§6§l!§f] §f史莱姆成功转职为 §b史莱姆法师"
          - job:data object set 还需训练时长/秒 10
          - job:data object set 所转职业 法师
          - job:entity collision all 2
          - job:object name self §b史莱姆法师
          - job:script stop

  "§6史莱姆剑士":
    type:
      - LEFT_CLICK
    1:
      - condition:
          - check "${job:object *data *正在训练的玩家}" != "%player_name%"
        condition-is-met:
          - send "§f[§6§l!§f] §f${job:object *data *正在训练的玩家} 正在这里训练他的史莱姆"
          - job:script stop
    2:
      - condition:
          - check "${job:object *data *还需训练时长/秒}" > 0
        condition-is-met:
          - send "§f[§6§l!§f] §6史莱姆剑士 §f训练时长还不够,再训练 ${job:object *data *还需训练时长/秒} 秒再来吧"
          - job:script stop
    3:
      - condition-is-met:
          - send "§f[§6§l!§f] §6史莱姆剑士 §f已经收回"
          - job:data object remove 还需训练时长/秒
          - job:data object remove 正在训练的玩家
          - job:data object remove 所转职业
          - job:entity collision all 1
          - job:object name all 史莱姆训练地


  "§b史莱姆法师":
    type:
      - LEFT_CLICK
    1:
      - condition:
          - check "${job:object *data *正在训练的玩家}" != "%player_name%"
        condition-is-met:
          - send "§f[§6§l!§f] §f${job:object *data *正在训练的玩家} 正在这里训练他的史莱姆"
          - job:script stop
    2:
      - condition:
          - check "${job:object *data *还需训练时长/秒}" > 0
        condition-is-met:
          - send "§f[§6§l!§f] §b史莱姆法师 §f训练时长还不够,再训练 ${job:object *data *还需训练时长/秒} 秒再来吧"
          - job:script stop
    3:
      - condition-is-met:
          - send "§f[§6§l!§f] §b史莱姆法师 §f已经收回"
          - job:data object remove 还需训练时长/秒
          - job:data object remove 正在训练的玩家
          - job:data object remove 所转职业
          - job:entity collision all 1
          - job:object name all 史莱姆训练地

tasks:
  "史莱姆训练":
    type: "CONTENT"
    run-type: "CYCLE"
    run-time: 1
    run-auto: true
    action-steps:
      1:
        - condition:
            - check "${job:object *data *还需训练时长/秒}" >= 1
          condition-is-met:
            - job:data object take 还需训练时长/秒 1
```
