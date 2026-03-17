# 工作组

## 介绍

所有 **工作对象设置都基于所属工作组** 所以这是插件最主要的一部分，了解这一部分内的配置后面的内容都可以轻松理解，同时你也可以查看 [插件示例&视频](../cha-jian-shi-li-shi-pin/) 页内容

## 对象类型基础设置

对象类型分为 **ENTITY、BLOCK** 两种类型，可通过工作组预设基础内容，后通过对象生成命令生成对象，具体请查看 [**工作对象生成**](../gong-zuo-dui-xiang/#dui-xiang-sheng-cheng)

ENTITY 类型设置 ([类型列表](dui-xiang-shi-ti-fang-kuai-lei-xing.md))

```yaml
basic-entity:
  #工作对象实体碰撞箱大小,实体为史莱姆 (仅类型为 entity 时)
  - entity-collision-size: 1
    #实体类型
    entity-type: "ZOMBIE"
    #生成实体的名字(可配合萌芽、龙核实体模型)
    default-name: "未命名"
```

BLOCK 类型设置 ([类型列表](dui-xiang-shi-ti-fang-kuai-lei-xing.md))

```yaml
basic-block:
    #方块类型
  - type: CREEPER_HEAD
    #默认对象显示名
    #因为是方块实体,所以对象显示名不会显示在方块上方,但对象占位符、动作脚本都可以读取到
    default-name: "未命名"
    #当 TYPE 为 CREEPER_HEAD 时生效,修改头颅名字(可兼容萌芽、龙核方块模型)
    default-skull-name: "model:grass"
```

## **工作步骤**

每当玩家对一个工作对象交互都会按照工作组内配置的步骤顺序处理下去，可以 **根据对象显示名不同执行不同预先设置的步骤** 同时可做到不同玩家处理不同步骤，对象显示名可通过 [**Object**](../gong-zuo-dui-xiang/dui-xiang-dong-zuo-jiao-ben/object.md) 对象动作脚本修改(不同玩家可以显示不同的名字)

```yaml
#动作处理步骤
action-steps:
  #对象显示名 (玩家对象显示名为杂草堆时就会触发这个步骤)
  "杂草堆":
    #模糊匹配 (开启后先效精准匹配再模糊匹配)
    #模糊匹配开启后只要显示名包含 杂草堆 即可触发
    fuzzy: true
    #交互触发方式
    type:
      - RIGHT_CLICK
      - LEFT_CLICK
    #步骤按 1~N 的顺序依次执行
    1:
        #触发条件
      - condition:
        - ...
        #满足条件时触发
        condition-is-met:
        - ...
        #不满足条件时触发
        condition-not-met:
        - ...
    #第二步骤
    2:
      #按照上面格式举一反三
      - ...
  #当对象显示名改为 杂草 时将不执行 杂草堆 预设步骤
  "杂草":
    #与上面配置格式相同，举一反三
```

{% hint style="info" %}
从 **1.0.8** 版本起支持 **对象持续交互** 可做到玩家与对象持续交互多长时间后触发脚本内容(移动时中断)，具体请查看 [**对象持续交互模块**](dui-xiang-chi-xu-jiao-hu-mo-kuai.md)\
\
效果视频: [http://file.yiyuen.com/file/download/333644](http://file.yiyuen.com/file/download/333644)
{% endhint %}

## 工作任务

每个工作组可预先设置不同的工作任务，任务分为 **延迟(DELAY)、循环(CYCLE)** 类型，处理类型分为**CONTENT OBJECT PLAYER** 三类，具体请查看 [**详细说明**](../gong-zuo-dui-xiang/dui-xiang-dong-zuo-jiao-ben/task.md#chu-fa-lei-xing) 预设好的工作可通过对象动作脚本内的 [**Task** ](../gong-zuo-dui-xiang/dui-xiang-dong-zuo-jiao-ben/task.md)脚本触发

```yaml
tasks:
  "任务名":
    #触发类型请查看上方链接
    type: "CONTENT"
    #任务类型
    #CYCLE - 循环运行任务
    #DELAY - 延迟运行任务
    run-type: "CYCLE"
    #延迟运行时间、循环运行间隔时间
    run-time: 5
    #自动运行(工作组加载时就运行,默认FALSE) 可选参数
    #仅触发类型为 CONTENT 时生效
    run-auto: true
    #所有对象数据 (默认开启状态) 可选参数
    #开启后任务触发会根据服务器内所属该对象数量,全部触发一遍
    #开启后可使用 object 对象相关的脚本
    #仅触发类型为 CONTENT 时生效
    object-data: true
    #是否对服务器内所有在线玩家触发 (默认FALSE) 可选参数
    #仅触发类型为 OBJECT、CONTENT 时生效
    online-player-run: false
    #处理步骤(与上方介绍大致相同)
    action-steps:
      1:
        - condition: 
            - ...
          condition-is-met:
            - ...
          condition-not-met:
            - ...
```

