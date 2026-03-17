---
description: 全息动作脚本
---

# Hologram

{% hint style="info" %}
参数内的 **{all/self}** 如果是 **ALL** 则为 **公共全息(全部可见)，**&#x4E3A; **SELF** 时则为 **私有全息(触发玩家可见)**
{% endhint %}

<details>

<summary>更新全息数据</summary>

job:hologram update **{all/self}**

</details>

<details>

<summary>发送更新全息内容</summary>

job:hologram send **{all/self} {name}**

**\[!]** 如果为 **SELF** 那么发送的全息仅触发者可见,需要安装 **ProtocolLib** 插件,会覆盖掉原有的全息内容

</details>

<details>

<summary>删除全息内容</summary>

job:hologram delete **{all/self}**

</details>

<details>

<summary>设置全息可见</summary>

job:hologram visible **{all/self} {true/false}**

</details>
