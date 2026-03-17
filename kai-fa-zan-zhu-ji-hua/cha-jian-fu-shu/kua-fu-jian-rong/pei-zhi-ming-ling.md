---
description: BungeeCord
---

# 配置&命令

## BungeeCord 配置

```yaml
setting:
  #延迟启动地牢,为了确保每个玩家都已经连接至对应地牢子服
  #建议 3~5 秒
  delay: 5
  #在这里设置 BungeeCord 主服
  main-server: "主服"

#地牢设置
dungeon:
  #当玩家再 BungeeCord 大厅输入 dl start <地牢名> 时将
  #自动传送至所设子服服务器并创建地牢,地牢结束后返回 BungeeCord 大厅
  #需在 BungeeCord 配置内设置对应子服服务器名称,并填至下方
  "地牢名": "子服"
```

以上配置 "地牢名": **"子服"** 需要对应子服上 **config.yml** 配置上 **bungee-cord** 中的 **channel** 所设内容，同时确保 **enable** 状态为 **true**

```yaml
#BungeeCord 跨服挑战地牢
#需要安装 BungeeCord 所用附属插件
bungee-cord:
  - enable: true
    #与 BungeeCord 插件配置对应
    channel: "子服"
```

## 命令

| 命令                           | 说明                                    |
| ---------------------------- | ------------------------------------- |
| dl start **<地牢> <启动参数(选填)>** | 启动跨服地牢 (离开地牢请使用子服上的 **/dp leave 命令**) |
|                              |                                       |
| dl team create               | 创建队伍                                  |
| dl team disband              | 解散队伍                                  |
| dl team quit                 | 退出队伍                                  |
| dl team kick **<玩家名>**       | 踢出队员                                  |
| dl team request **<玩家名>**    | 请求加入某个玩家的队伍                           |
| dl team accept **<玩家名>**     | 接受某个玩家的入队申请                           |

