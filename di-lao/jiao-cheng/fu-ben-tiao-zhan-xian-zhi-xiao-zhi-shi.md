# 副本挑战限制小知识

## 限制地牢组队挑战人数

插件上有 [**Team-Condition**](https://ersha.gitbook.io/dungeonplus/di-lao/untitled/jiao-ben-lie-biao/tiao-jian-pan-duan-lei/team-condition) 脚本，如果不满足该脚本所设下限人数或上限人数就无法调整地牢

```yaml
地牢 Option.yml 配置内容
#地牢启动时
dungeon-start:
  #启动条件,条件满足是将传送至地牢内并执行 actionScript 脚本内容
  condition: 
  - "$team-condition{team=true;min=3;max=5;message=队伍必须3人以上才可挑战,当前队伍人数 (<size>)} @system"
  #启动条件满足时触发
  action-script: []
```

## 挑战入场卷设置

从 **1.0.8** 新增的地牢占位符功能有 [**Item**](https://ersha.gitbook.io/dungeonplus/di-lao/di-lao-zhan-wei-fu/item) 占位符，使用 [**Js-Condition**](https://ersha.gitbook.io/dungeonplus/di-lao/untitled/jiao-ben-lie-biao/tiao-jian-pan-duan-lei/untitled-2) 脚本配合该占位符即可做到收取挑战入场卷的功能

```yaml
地牢 Option.yml 配置内容
#地牢启动时
dungeon-start:
  #启动条件,条件满足是将传送至地牢内并执行 actionScript 脚本内容
  condition: 
  - "$js-condition{text='<item:测试物品 *1 *true>'=='true';message=队伍内有队员缺少 [测试物品]*1 无法开启地牢} @system"
  #启动条件满足时触发
  action-script: []
```
