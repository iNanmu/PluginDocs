---
description: 自定义对象生成刷新点
---

# 刷新点

## 介绍

该功能可以让你做到 **自定义每一个区域** 或 **自定义世界某个范围** 内刷新指定的工作对象，同时可以设置刷新点刷新数量的上限、每次刷新的数量，刷新对象是不会属性在海面上。

刷新点相关配置位于 **./refresh** 文件夹内

```yaml
refresh-name: "一号刷新点"
refresh-content:
  #区域对象刷新时间间隔/分钟
  time: 10
  #刷新提示
  refresh-message: true
  #刷新的世界
  refresh-world: "world"
  #全世界随机,从 -2000 ~ 2000 随机X位置
  refresh-x: 2000
  #全世界随机,从 -2000 ~ 2000 随机Z位置
  refresh-z: 2000
  #区域刷新对象数据来源
  content:
    蓝水晶矿-ENTITY:
      #工作组名
      name: "蓝水晶矿"
      #刷新的实体类型
      type: ENTITY
      #单次刷新数量
      single-number: 3
      #刷新数量上限
      ceiling-number: 10
  #区域位置 (AB点)
  #删掉的话则以整个世界内随机刷新(不建议,因为你可能找不到)
  #设置后上方 refresh-x,refresh-z 失效
  #location:
  #  low:
  #    world: world
  #    x: 1790.0
  #    y: 62.0
  #    z: 985.0
  #    pitch: 45.599937
  #    yaw: -33.9001
  #  high:
  #    world: world
  #    x: 1797.0
  #    y: 69.0
  #    z: 992.0
  #    pitch: 45.599937
  #    yaw: -33.9001
```
