---
description: 方块对象动作脚本
---

# Block

{% hint style="info" %}
参数内的 **{all/self}** 如果是 **ALL** 则对服务器内全部玩家触发，为 **SELF** 时则只有触发玩家触发
{% endhint %}

<details>

<summary>修改对象显示名</summary>

job:block name **{all/self} {name}**

**\[!]** 因为是 **方块类型** 所以不会显示出来但占位符啥的都可以读取到

</details>

<details>

<summary>修改对象方块类型</summary>

job:block type **{all/self} {material}** ([类型列表](../../gong-zuo-zu/dui-xiang-shi-ti-fang-kuai-lei-xing.md)）

</details>

<details>

<summary>修改头颅数据内容</summary>

job:block skull-owner **{all/self} {name}**

**\[!]** 这个主要是用来兼容 **萌芽、龙核** 的方块模型功能，设为 "model:模型名" 即可替换

</details>
