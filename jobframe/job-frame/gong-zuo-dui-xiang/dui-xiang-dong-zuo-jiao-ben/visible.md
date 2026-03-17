---
description: 对象可见动作脚本
---

# Visible

{% hint style="info" %}
参数内的 **{all/self}** 是 **ALL** 则对服务器内全部玩家触发，为 **SELF** 时则只有触发玩家触发\
参数内的 **{content/object}** 是 **CONTENT** 则以工作组内的所有对象触发，为 **OBJECT** 时则以触发的工作对象触发，不影响其他对象
{% endhint %}

<details>

<summary>修改对象可见设置</summary>

job:visible **{all/self} {content/object} {true/false}**

**\[!]** 方块、实体都可以修改可见设置,不同玩家的设置互不干扰

</details>

