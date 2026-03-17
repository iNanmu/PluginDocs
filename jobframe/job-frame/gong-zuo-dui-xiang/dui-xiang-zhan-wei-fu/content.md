---
description: 工作组占位符
---

# Content

<details>

<summary>获取数据储存器内的数据 (Data)</summary>

${job:content \*data **\*{key}** _\*{type} \*{default}_}&#x20;

{type} 有 **str(文本) int(整数)** **date(时间格式)** **date-time(秒数)** (可选参数)

{default} 则 **是当没有该数据时返回的值** (可选参数)\
\
\
当 {type} 为 **date** 时，如果数据符合时间格式转换将返回 `'yyyy-MM-dd/HH:mm:ss'`

当 {type} 为 **date-time** 时，如果数据储存为时间戳将返回 `'倒计时秒数'`

**返回:** 储存的数据 ( 不存在时返回 "默认值参数所赋予的值,无则默认 none " )

**\[!]** 所有属于该工作组内的对象数据共享,玩家数据共享

</details>

<details>

<summary>获取数据储存器内的临时数据 (Temp-Data)</summary>

${job:content \*temp-data **\*{key}** _\*{type} \*{default}_}

{type} 有 **str(文本) int(整数)** **date(时间格式)** **date-time(秒数)** (可选参数)

{default} 则 **是当没有该数据时返回的值** (可选参数)\
\
\
当 {type} 为 **date** 时，如果数据符合时间格式转换将返回 `'yyyy-MM-dd/HH:mm:ss'`

当 {type} 为 **date-time** 时，如果数据储存为时间戳将返回 `'倒计时秒数'`

**返回:** 储存的数据 ( 不存在时返回 "默认值参数所赋予的值,无则默认 none " )

</details>

<details>

<summary>获取组UUID</summary>

${job:content \*uuid}

**返回:** UUID

</details>

<details>

<summary>获取组名</summary>

${job:content \*name}

**返回:** 唯一名

</details>

<details>

<summary>获取组内对象数量</summary>

${job:content \*object-size}

**返回:** 工作组内已在服务器生成的对象

</details>
