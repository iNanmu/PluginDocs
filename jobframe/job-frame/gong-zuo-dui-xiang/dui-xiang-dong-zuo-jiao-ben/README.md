# 对象动作脚本

## 介绍

插件采用 **脚本的方式运行** 自身带有脚本功能同时支持调用 **Kether** 脚本，插件自身的脚本一般以 **"JOB:"** 开头，而 **Kether** 脚本则按 **Kether** 对应脚本语法输入，Kether 脚本列表请在此 [**页面**](https://kether.tabooproject.org/list.html) 查看

## 概率执行格式

为某一行 **动作脚本行** 或 **Kether脚本行** 设置单独的触发概率，格式如下

`'job:visible self object false ~@0.5'` 有 50% 概率触发该行脚本

`'command "fly" as op ~@0.5'` 有 50% 概率触发该行脚本

只需要在脚本行后面加上 **\~@0.0-1.0** 即可

## 基础配置格式

```yaml
#触发条件
condition:
  #Kether
  - if check placeholder *"%player_hand_name%" == *"超级除草刀"
#条件满足时触发
condition-is-met:
  #Kether
  - send *"&6超级杂草 &f成功被移除"
  #Job Script
  - job:object name self 杂草堆
#条件不满足时触发
condition-not-met:
  #Kether
  - send *"你需要手持 &6超级除草刀"
```
