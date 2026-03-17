---
description: 临时数据动作脚本
---

# Temp-Data

{% hint style="warning" %}
注意该脚本所储存的数据将 **不会储存至数据库**，仅做临时数据使用，如果你需要你的数据被持久化储存并跨服同步，请使用 **Data** 动作脚本，使用该脚本你无需像 **Data** 脚本一样小心翼翼
{% endhint %}

| 类型      | 说明                               |
| ------- | -------------------------------- |
| CONTENT | 储存至工作组上 (所有工作对象都可以读取)            |
| OBJECT  | 储存至单个工作对象                        |
| PLAYER  | 储存至玩家数据内的触发对象数据存储器，不同对象存储器不同互不干扰 |

<details>

<summary>修改数据</summary>

job:temp-data **{content/object/player} {set/add/take} {key} {value}**

**\[!]** 储存内容为字符时无法使用 add、take 操作,为数值时才可以使用

</details>

<details>

<summary>删除数据</summary>

job:temp-data {content/object/player} remove {key}

</details>

<details>

<summary>删除数据名包含指定字符的数据</summary>

job:temp-data {content/object/player} remove-contains {str}

* 例如 job:data content set **%player\_name%-玩家名** true 储存的数据名 **每个玩家都不同**
* 如果需要删除数据的时候 job:data content remove-contains **玩家名** 即可清除包含,数据
* 名包含 **玩家名** 的数据

</details>
