---
description: 任务动作脚本
---

# Task

## 处理类型

| 类型      | 说明                                                                                                                                |
| ------- | --------------------------------------------------------------------------------------------------------------------------------- |
| CONTENT | 任务触发时将以工作组内的 **所有对象** 并以服务器内 **所有玩家为触发者** 触发                                                                                      |
| OBJECT  | 以 **执行的对象** 并以服务器内 **所有玩家为触发者** 触发                                                                                                |
| SELF    | <p>以 <strong>执行的对象</strong> 并以 <strong>触发的玩家为触发者</strong> 触发<br>该类型下会将任务储存至玩家数据,玩家离线也会在下次登录时触发,前提该对象需要是 <strong>持久对象</strong></p> |



<details>

<summary>执行任务</summary>

job:task perform **{content/object/player}** **{task}**

</details>

<details>

<summary>结束任务</summary>

job:task cancel **{content/object/player} {task}**

</details>

<details>

<summary>直接触发</summary>

job:task trigger **{content/object/player} {task}**

**\[!]:** 这个脚本触发的任务是 **瞬间触发** 不管是 **延迟还是循环任务** 都只触发一次

</details>
