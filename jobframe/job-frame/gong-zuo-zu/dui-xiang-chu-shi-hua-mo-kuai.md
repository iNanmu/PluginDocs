---
description: 额外扩展配置模块
---

# 对象初始化模块

## 作用

对象首次生成至服务器时触发，一般用于设置一些对象数据或启动某些对象任务所使用

## 配置

与其他位置上的动作脚本处理步骤相同，都是按照顺序执行下去

```yaml
#对象第一次加载到服务器上时触发脚本动作处理 (无玩家)
init-action:
  0:
    - condition-is-met:
        #设置生长时长 growth_time 为 10
        - 'job:data object set growth_time 10'
        #启动 蓝水晶生长周期 任务
        - 'job:task perform object 蓝水晶生长周期'
```
