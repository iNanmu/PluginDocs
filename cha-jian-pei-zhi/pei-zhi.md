---
description: 地牢数据配置位于 /dungeon 文件夹中
---

# 地牢配置

## Option.yml

> 地牢基础内容设置

```yaml
#地牢启动时初始化
dungeon-init-script: []

#地牢启动时
dungeon-start:
  #启动条件,条件满足是将传送至地牢内并执行 actionScript 脚本内容
  condition: []
  #启动条件满足时触发
  action-script: []

#地牢通关时触发
dungeon-reward-script: []
```

## Obstacle.yml

> 地牢障碍组配置，障碍组需通过 **Obstacle** 脚本进行触发

```yaml
obstacles:
  #默认障碍组
  default:
      #障碍物数据
    - obstacle-block: []
      #障碍组触发时执行
      action-script: []
  
  #默认障碍组
  #第N个:
      #障碍物数据
    #- obstacleBlock: []
      #障碍组触发时执行
    #  actionScript: []
```

## Monster.yml

> 地牢怪物组配置，怪物组需通过[ **MonsterGroup** ](https://ersha.gitbook.io/dungeonplus/untitled/jiao-ben-lie-biao/guai-wu-zu-lei/monstergroup)脚本进行触发

```yaml
groups:
  #默认怪物组
  default:
    #怪物数据
  - monster: []
    #条件
    condition: []
    #怪物组触发时执行
    start: []
    #条件达成是触发
    end: []
    #地牢启动时自动运行怪物组,默认关闭
    #关闭状态下想要通过 MonsterGroup 脚本进行启动
    auto-start: false
  
  #默认怪物组
  #第N个:
    #怪物数据
  #- monster: []
    #条件
  #  condition: []
    #怪物组触发时执行
  #  start: []
    #条件达成是触发
  #  end: []
```

## Task

> 地牢任务 位于 **/dungeon/地牢/task** 文件夹内，在文件夹内建立任意名称的 **yml** 配置即可,支持 **定时或循环** 执行

```yaml
#请使用 $task 脚本进行操作,具体请查看 WIKI 的 ActionScript 介绍

task:
  # 时间 / 秒
  - 2:
    # 触发的脚本
    - "$message{type=text;text=<player.name> 时间过去了两秒} @player"
    10:
    # 触发的脚本
    - "$message{type=text;text=<player.name> 时间过去了十秒} @player"
    #time:
    #- actionscript 脚本
```

## Interace

> 地牢交互 位于 **/dungeon/地牢/interact** 文件夹内，在文件夹内建立任意名称的 **yml** 配置即可

```yaml
#交互类型
type: PLACE
#是否只执行一次
first: true
#参数，每个交互类型的参数都不同，具体查看 WIKI 的 DungeonInteract 介绍
parameter:
  location: -5.0,51.0,-28
  blockName: 能量块
#触发时执行的脚本
script:
- $obstacle{group=障碍物一;operation=delete} @dungeon
```

