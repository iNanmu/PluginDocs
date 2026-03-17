---
description: Action
---

# 工艺动作组

## 介绍

插件上的运行全部依靠 Action 来运作，所以你要学会使用这个插件，你就得理解  Action  的运行方式及逻辑，同时插件支持 Kether 语法触发，插件 Action 格式均为 **"craft:action \*params"** 不带 **craft:** 开头的视为 Kether 语法运行

## 基础格式

一个最基础的 Action 配置为以下格式，这个格式内 condition、meet、not-meet 都是可选的，你可以只设置 meet 那样子该 Action 配置就必定会触发 meet 所设内容

```yaml
- condition:
    #条件判断,这里的条件满足于不满足分别会执行 meet 或 not-meet 内所设 action 脚本
    #插件支持使用 Kether 的所有语法
    - "XXXX"
  #上方条件满足时触发
  meet:
    - "XXXX"
  #上方条件不满足时触发
  not-meet:
    - "XXXX"
```

## 进阶格式

以 **工艺图纸** 配置内的 start-actions 配置项为例，他会按步骤顺序依次往下执行，这个格式仅在 start-actions、extract-actions 配置项上使用，工艺图纸配置的 actions 项，请看下文 **高级进阶格式** 写法

```yaml
start-actions:
  #步骤1
  1:
    - condition:
      - "XXXX"
    meet:
      - "XXXX"
    not-meet:
      - "XXXX"
  #步骤2
  2:
    - condition:
      - "XXXX"
    meet:
      - "XXXX"
    not-meet:
      - "XXXX"
```

## 高级进阶格式

这个写法只在 工艺图纸 配置上的 actions 配置项使用，这个会把 Action 动作组分为 主、子 的步骤运行，一个主的 Action 动作组内可以包含多个子的 Action 动作组

```yaml
actions:
  #主步骤1
  1:
    #子步骤1
    1:
      - condition:
        - "XXXX"
      meet:
        - "XXXX"
      not-meet:
        - "XXXX"
    #子步骤2
    2:
      - condition:
        - "XXXX"
      meet:
        - "XXXX"
      not-meet:
        - "XXXX"
  #主步骤2
  2:
    #子步骤1
    1:
      - condition:
        - "XXXX"
      meet:
        - "XXXX"
      not-meet:
        - "XXXX"
    #子步骤2
    2:
      - condition:
        - "XXXX"
      meet:
        - "XXXX"
      not-meet:
        - "XXXX"
```

## 终止运行方式

在插件使用的过程中，如果需要做到概率判断不满足时中断 Action 动作组继续往下执行时可在 Action 动作组对应的配置位置中加上以下关键词做到终止

| 关键词         | 作用                     |
| ----------- | ---------------------- |
| cancel\_all | 终止接下来所有动作组的运行 (主、子都终止) |
| cancel\_sub | 终止子动作组内接下来的动作运行        |

**cancel\_sub** 在 **高级进阶格式** 上的用法比较特殊，如果是在动作组内使用该关键词，那么他会终止该主动作组内子动作组接下来步骤的运行，但不会运行到接下来运行到的主动作组，如果要终止接下来所有主动作组的运行，需要使用 **cancel\_all** 来终止

## 懂了吗？不懂接着往下看









































看得出你是真的不懂，所以建议你看下插件提供的例子，上面都有用到上面说的内容，我还写了详细的注释
