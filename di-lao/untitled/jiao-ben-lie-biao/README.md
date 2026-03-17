# 脚本列表

## 插件原生脚本列表

附属所注册的脚本不包含在内，可在游戏内查看附属注册的脚本或者由附属开发者提供\
别看原生的脚本不多，但已经可以完成绝大部分的游戏内容了

## INIT 类型

| 脚本             | 作用       |
| -------------- | -------- |
| setmap         | 设置地牢地图   |
| setspawn       | 设置地牢出生点  |
| setting        | 设置地牢基础设置 |
| revive-setting | 设置地牢复活设置 |

## DUNGEON 类型

| 脚本           | 作用                              |
| ------------ | ------------------------------- |
| command      | 执行命令                            |
| message      | 发送消息                            |
| data         | 地牢数据(DungeonMeta) 操作            |
| mob          | 在指定区域召唤怪物 (目前仅支持 MythicMobs 插件) |
| monstergroup | 触发某个怪物组内容                       |
| block        | 设置 \[区域1] 至 \[区域2] 两个点的障碍物区域    |
| obstacle     | 清除或恢复一个障碍组                      |
| interact     | 启动或结束指定的 DungeonInteract 交互脚本   |
| task         | 启动或结束指定的 DungeonTask 任务         |
| script       | 触发 ActionScript 脚本组             |
| end          | 结束地牢                            |
| teleport     | 传送                              |

## PLAYER 类型

| 脚本       | 作用                   |
| -------- | -------------------- |
| command  | 执行命令                 |
| message  | 发送消息                 |
| teleport | 传送                   |
| script   | 触发 ActionScript 脚本组  |
| data     | 地牢数据(DungeonMeta) 操作 |

## SELF 类型

| 脚本           | 作用                                                                                                                 |
| ------------ | ------------------------------------------------------------------------------------------------------------------ |
| command      | 执行命令                                                                                                               |
| message      | 发送消息                                                                                                               |
| teleport     | 传送                                                                                                                 |
| script       | 触发 ActionScript 脚本组                                                                                                |
| data         | 地牢数据(DungeonMeta) 操作                                                                                               |
| js-condition | <p>JavaScript 条件判断(支持PAPI变量)<br>类型为 <strong>@system</strong> 则判断整个地牢内的玩家<br>类型为 <strong>@self</strong> 时则判断触发者</p> |

## SYSTEM 类型

| 脚本             | 作用                                                                                                                 |
| -------------- | ------------------------------------------------------------------------------------------------------------------ |
| kill           | 判断 地牢内击杀某种怪物到一定数量 完成                                                                                               |
| taskcontain    | 判断地牢内某个 DungeonTask 任务是否正在运行                                                                                       |
| data-condition | 判断 地牢数据(DungeonMeta) 内容                                                                                            |
| js-condition   | <p>JavaScript 条件判断(支持PAPI变量)<br>类型为 <strong>@system</strong> 则判断整个地牢内的玩家<br>类型为 <strong>@self</strong> 时则判断触发者</p> |
