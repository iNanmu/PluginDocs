---
description: 工作对象占位符
---

# Object

{% hint style="info" %}
该占位符数据来源于触发的对象，对象之间的数据 **互不干扰**
{% endhint %}

<details>

<summary>获取数据储存器内的数据 (Data)</summary>

${job:object \*data **\*{key}** _\*{type} \*{default}_}&#x20;

{type} 有 **str(文本) int(整数)** **date(时间格式)** **date-time(秒数)** (可选参数)

{default} 则 **是当没有该数据时返回的值** (可选参数)\
\
\
当 {type} 为 **date** 时，如果数据符合时间格式转换将返回 `'yyyy-MM-dd/HH:mm:ss'`

当 {type} 为 **date-time** 时，如果数据储存为时间戳将返回 `'倒计时秒数'`

**返回:** 储存的数据 ( 不存在时返回 "默认值参数所赋予的值,无则默认 none " )

**\[!]** 存储器内数据所有玩家共享

</details>

<details>

<summary>获取数据储存器内的临时数据 (Temp-Data)</summary>

${job:object \*temp-data **\*{key}** _\*{type} \*{default}_}

{type} 有 **str(文本) int(整数)** **date(时间格式)** **date-time(秒数)** (可选参数)

{default} 则 **是当没有该数据时返回的值** (可选参数)\
\
\
当 {type} 为 **date** 时，如果数据符合时间格式转换将返回 `'yyyy-MM-dd/HH:mm:ss'`

当 {type} 为 **date-time** 时，如果数据储存为时间戳将返回 `'倒计时秒数'`

**返回:** 储存的数据 ( 不存在时返回 "默认值参数所赋予的值,无则默认 none " )

</details>

<details>

<summary>获取对象UUID</summary>

${job:object \*uuid}

**返回:** UUID

</details>

<details>

<summary>获取对象ID</summary>

${job:object \*id}

**返回:** 唯一ID

</details>

<details>

<summary>获取对象所在位置</summary>

${job:object \*location}

**返回:** X,Y,Z

${job:object \*x}

**返回:** X

${job:object \*y}

**返回:** Y

${job:object \*z}

**返回:** Z

</details>
