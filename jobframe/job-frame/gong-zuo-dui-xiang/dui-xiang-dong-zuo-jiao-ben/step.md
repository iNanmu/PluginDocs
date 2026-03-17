---
description: 步骤组交互动作脚本
---

# Step

{% hint style="info" %}
该脚本内所有执行对象一定是触发对象的玩家
{% endhint %}

<details>

<summary>为玩家触发某个已配置的步骤组</summary>

job:step cast **{name}**

这里的 **{name}** 必须是已经在工作组内 **action-steps** 配置内设置的节点名

```yaml
#动作步骤
action-steps:
  #使用 job:step cast 特殊步骤组 即可为玩家触发该步骤组内所设脚本
  "特殊步骤组":
    #通过setp脚本触发的步骤组不需要 type 配置
    1:
      - condition-is-met:
          - send *"§f[§6§l!§f] §b你触发了特殊步骤组"
```

</details>
