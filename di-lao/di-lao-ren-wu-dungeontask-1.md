---
description: DungeonMonster
---

# 地牢怪物

## 说明

目前支持生成 MythicMobs 4.X/5.X 版本插件怪物

## 怪物组的设置方式

怪物组配置位于地牢配置文件夹 **monster.yml** 配置中，可设置多个怪物组

```yaml
groups:
  #默认怪物组
  default:
    #怪物数据 (一般都是属于 mob 脚本生成)
  - monster: []
    #条件 (满足条件后会触发下方 end 内所设脚本)
    condition: []
    #怪物组触发时执行
    start: []
    #条件达成是触发
    end: []
    #地牢启动时自动运行怪物组,默认关闭
    #关闭状态下需要通过 MonsterGroup 脚本进行启动
    auto-start: false
```

如何做到 **一波一波的怪物刷新** 呢

```yaml
groups:
  #默认怪物组
  default:
  - monster:
    - $mob{plugin=MythicMobs;name=MM怪物节点名;location=1804.0,3.0,964.0;amount=4;scattered=1} @dungeon
    condition:
    #这里的怪物名是上方召唤怪物的名字,不要输入成节点名
    #这个脚本的作用是判断在地牢内击杀的怪物数量
    - $kill{mobname=怪物名;amount=4} @system
    start: []
    #当 condition 条件满足时触发下方脚本 (每次在地牢内击杀怪物触发检测)
    end:
    #五秒后重新刷新 default 这个怪物组
    - $monstergroup{group=default;repeat=true;delay=5} @dungeon
    #地牢启动时自动运行怪物组,默认关闭
    #关闭状态下需要通过 MonsterGroup 脚本进行启动
    auto-start: true
```

## 怪物组要如何触发

为了更加灵活的操作地牢内的流程，地牢怪物组设置好后不会在地牢运行时启动执行，你需要使用 **$monstergroup** 脚本来操作，例如 **"$monstergroup{group=default;repeat=true;delay=5} @dungeon"** 来执行触发操作，你也可以通过配置上的 **auto-start** 项目做到地牢启动时自启交互组
