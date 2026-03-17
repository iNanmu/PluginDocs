---
description: 从 1.1.4 版本起支持该功能
---

# 地牢区域

## 说明

一个地牢可以设置多个地牢区域，你可以让某些 **脚本只对某个区域内的玩家触发效果** 也可以通过地牢占位符来 **获取一个地牢区域内的玩家数量(AREA)、获取一个玩家所在的地牢区域(SELF)** 等，开发者也可以获取区域内的某些数据，如玩家等

## 地牢区域设置

地牢区域配置是在 **OPTION.YML** 配置文件中，每个地牢的地牢区域都是独立，一个地牢区域是由 **A / B** 点组成的正方形区域，区域名不可重复，需要按照配置内的格式设置

```yaml
#地牢启动时初始化
dungeon-init-script: []

#地牢启动时
dungeon-start:
  #启动条件,条件满足是将传送至地牢内并执行 actionScript 脚本内容
  condition: []
  #启动条件满足时触发
  action-script: []

#地牢区域设置
dungeon-area: []
  #- "TEST-AREA": "X,Y,Z/X,Y,Z"
  #  "TEST-AREA2": "X,Y,Z/X,Y,Z"

#地牢通关时触发
dungeon-reward-script: []
```

```yaml
#地牢区域设置
dungeon-area: []
  #格式一定要是这样子，不要多加 - 也不要不加 - 就加一个 -
  - "TEST-AREA": "X,Y,Z/X,Y,Z"
    "TEST-AREA2": "X,Y,Z/X,Y,Z"
```
