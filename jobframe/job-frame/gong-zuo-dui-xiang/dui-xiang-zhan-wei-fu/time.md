---
description: 时间占位符
---

# Time

<details>

<summary>获取当前时间戳</summary>

${job:time \*current \*time}

{time} 为额外增加的时间 (可选参数)<br>

例子：\
`${job:time *current}` 返回当前时间戳

`${job:time *current *10}` 返回十秒后的时间戳

**返回:** min \~ max 的随机值

</details>

<details>

<summary>获取当前时间格式</summary>

${job:time \*date \*time}

{time} 为额外增加的时间 (可选参数)\
\
例子：\
`${job:time *date}` 返回 2022/12/07:00:00:00

`${job:time *date*10}` 返回 2022/12/07:00:00:10

**返回:** 格式为 'yyyy-MM-dd/HH:mm:ss 的字符串

</details>
