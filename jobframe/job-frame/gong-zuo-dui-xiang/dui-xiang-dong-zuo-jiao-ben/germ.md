---
description: 萌芽动作脚本
---

# Germ

{% hint style="info" %}
参数内的 **{all/self}** 如果是 **ALL** 则对服务器内全部玩家触发，为 **SELF** 时则只有触发玩家触发
{% endhint %}

<details>

<summary>播放模型动画</summary>

job:germ animation **{start/clear} {all/self} {name} {delay}**

**{dealy}** 运行多久自动停止播放，为 -1 或 空 时只能通过 **clear** 操作清除动画播放

</details>
