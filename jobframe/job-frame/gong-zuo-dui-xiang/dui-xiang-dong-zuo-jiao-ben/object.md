---
description: 对象动作脚本
---

# Object

{% hint style="info" %}
参数内的 **{all/self}** 如果是 **ALL** 则对服务器内全部玩家触发，为 **SELF** 时则只有触发玩家触发
{% endhint %}

<details>

<summary>修改对象显示名</summary>

job:object name **{all/self} {name}**

**\[!]** 不管对象是 **BLOCK,ENTITY** 的对象类型都可以使用这个脚本 (自动识别对象类型)

</details>

<details>

<summary>修改对象显示实体&#x26;方块类型</summary>

job:object type **{all/self} {type}** ([类型列表](../../gong-zuo-zu/dui-xiang-shi-ti-fang-kuai-lei-xing.md))

**\[!]** 不管对象是 **BLOCK,ENTITY** 的对象类型都可以使用这个脚本 (自动识别对象类型)

</details>

<details>

<summary>永久删除对象</summary>

job:object delete

</details>

<details>

<summary>临时删除对象</summary>

job:object temp-delete

**\[!]** 临时删除对象只适用于持久对象,临时删除后重启服务器还会生成

</details>
