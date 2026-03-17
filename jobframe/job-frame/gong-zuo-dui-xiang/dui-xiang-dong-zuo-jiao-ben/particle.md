---
description: 粒子显示动作脚本
---

# Particle

{% hint style="info" %}
参数内的 **{all/self}** 如果是 **ALL** 则对服务器内全部玩家触发，为 **SELF** 时则只有触发玩家触发
{% endhint %}

<details>

<summary>发送粒子显示</summary>

job:particle **{all/self} {type} {particle} {range}**

</details>

### {type}:

|  类型    | 说明        |
| ------ | --------- |
| STAR   | 发送一个星形粒子  |
| CUBE   | 发送一个正方形粒子 |
| CIRCLE | 发送一个圆形粒子  |
| SPHERE | 发送一个球形粒子  |

### {particle}:

不同版本的 Particle 类型不一样，具体的枚举可以通过该文档查看 [BukkitDoc](https://bukkit.windit.net/javadoc/org/bukkit/Particle.html) (这是最新版的类型,可能旧版本服务器也可以用,如果没法用请下载 [1.12.2](https://dr.windit.net/release.zip)/[1.13+](https://dr.windit.net/master.zip) 离线版，后找到 **Particle** 页面即可

### {range}:

半径、范围、大小
