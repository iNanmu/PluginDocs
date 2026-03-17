# 自定义动作组

## 介绍

每个工艺图纸配置内都可设置 **自定义动作组** 该功能主要用于节省配置编辑重复率，即大部分相同的配置可以写成一个 **自定义动作组** 然后在需要用到的地方使用 `craft:system *perform-actions *自定义组名 *运行次数` 执行该自定义组，这样子可以节省很多时间，不用重复写一样的配置内容

## 使用方式

该功能采用的动作运行格式为 [高级进阶格式](../gong-yi-dong-zuo-zu/#gao-ji-jin-jie-ge-shi) 在工艺图纸配置内新增 **custom-actions** 配置项并编写即可

```yaml
custom-actions:
  #在需要使用的地方通过 craft:system *perform-actions *自定义组名A *1 脚本触发一次
  "自定义组名A":
    1:
      1:
        - condition:
            - xxx
          meet:
            - xxx
          not-meet:
            - xxx
  "自定义组名B":
    1:
      1:
        - condition:
            - xxx
          meet:
            - xxx
          not-meet:
            - xxx
```

你可以查看 [强化示例](../gong-yi-shi-li-pei-zhi/qiang-hua-shi-li.md) 的配置方法，强化示例有使用到该功能
