---
description: 实体对象动作脚本
---

# Entity

{% hint style="info" %}
参数内的 **{all/self}** 如果是 **ALL** 则对服务器内全部玩家触发，为 **SELF** 时则只有触发玩家触发
{% endhint %}

<details>

<summary>修改对象显示名</summary>

job:entity name **{all/self} {name}**

**\[!]** 仅为 **实体对象** 类型时生效,这就是与 **Object** 脚本不同的地方

</details>

<details>

<summary>修改对象显示实体类型</summary>

job:entity type **{all/self} {type}** ([类型列表](../../gong-zuo-zu/dui-xiang-shi-ti-fang-kuai-lei-xing.md))

**\[!]** 仅为 **实体对象** 类型时生效,这就是与 **Object** 脚本不同的地方&#x20;

</details>

<details>

<summary>修改对象碰撞箱大小</summary>

job:entity collision **{all/self} {value(1\~N)}**

**\[!]** 仅类型为史莱姆时生效

</details>
