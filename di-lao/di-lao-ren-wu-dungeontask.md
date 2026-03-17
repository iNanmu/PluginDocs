---
description: DungeonTask
---

# 地牢任务

## 说明

每个地牢都可以设置不同的任务处理，任务处理可以是循环处理也可以是定时处理\
任务的处理方式都是触发 **ActionScript** 脚本来完成，注意地牢任务 **没有触发者** 也就是说地牢任务上所执行的脚本不可以使用 **@SELF** 脚本类型

## 任务的设置方式

在地牢配置文件夹中的 **task** 文件夹内新增任意名称的 yml 配置，并按照以下格式输入即可

```yaml
#地牢启动时自动启动任务 (1.2.8+)
#未设置的任务想要通过 Task 地牢脚本进行启动
auto-start:
  #格式为 任务名 是否异步 运行模式
  - "任务一 false cycle"
  - "任务一 false timing"

#任务名可自定义,但一个地牢内的任务名不可重复,否则将会相互覆盖
任务一:
  # 时间 / 秒
  - 2:
    # 触发的脚本
    - "$message{type=text;text=<player.name> 时间又过去了两秒} @player"
    10:
    # 触发的脚本
    - "$message{type=text;text=<player.name> 时间又过去了十秒} @player"
    #time:
    #- actionscript 脚本

任务二:
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

## 任务要怎么开始执行？

为了更加灵活的操作地牢内的流程，地牢任务设置好后不会再地牢运行时启动执行，你需要使用 **$task** 脚本来操作，例如 **"$task{name=任务名;operation=start;async=true} @dungeon"** 来执行启动操作，当然你也可以通过在任务配置内添加 **auto-start** 配置来完成地牢启动时自启任务
