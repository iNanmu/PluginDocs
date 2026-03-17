---
description: 动作脚本
---

# Script

{% hint style="info" %}
参数内的 **{all/self}** 如果是 **ALL** 则对服务器内全部玩家触发，为 **SELF** 时则只有触发玩家触发
{% endhint %}

<details>

<summary>结束接下来的脚本运行</summary>

job:script stop

</details>

<details>

<summary>发送对象触发事件</summary>

job:script event {key} {data,data,..}

</details>
