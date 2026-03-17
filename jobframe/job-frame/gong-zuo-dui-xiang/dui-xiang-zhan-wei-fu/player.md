---
description: 玩家占位符
---

# Player

{% hint style="info" %}
该占位符数据来源于触发的对象，对象之间的数据互不干扰，**玩家之间数据也互不干扰**
{% endhint %}

<details>

<summary>获取数据储存器内的数据 (Data)</summary>

${job:player \*data **\*{key}** _\*{type} \*{default}_}

{type} 有 **str(文本) int(整数)** **date(时间格式)** **date-time(秒数)** (可选参数)

{default} 则 **是当没有该数据时返回的值** (可选参数)\
\
\
当 {type} 为 **date** 时，如果数据符合时间格式转换将返回 `'yyyy-MM-dd/HH:mm:ss'`

当 {type} 为 **date-time** 时，如果数据储存为时间戳将返回 `'倒计时秒数'`

**返回:** 储存的数据 ( 不存在时返回 "默认值参数所赋予的值,无则默认 none " )

</details>

<details>

<summary>获取数据储存器内的临时数据 (Temp-Data)</summary>

${job:player \*temp-data **\*{key}** _\*{type} \*{default}_}

{type} 有 **str(文本) int(整数)** **date(时间格式)** **date-time(秒数)** (可选参数)

{default} 则 **是当没有该数据时返回的值** (可选参数)\
\
\
当 {type} 为 **date** 时，如果数据符合时间格式转换将返回 `'yyyy-MM-dd/HH:mm:ss'`

当 {type} 为 **date-time** 时，如果数据储存为时间戳将返回 `'倒计时秒数'`

**返回:** 储存的数据 ( 不存在时返回 "默认值参数所赋予的值,无则默认 none " )

</details>

<details>

<summary>获取玩家当前触发对象显示名</summary>

${job:player \*visible-name}

**返回:** 名字

</details>

<details>

<summary>判断是否在对象半径周围内</summary>

${job:player \*check-range **\*{range(1\~N)}**}

**返回:** true/false

</details>

<details>

<summary>判断玩家背包内是否存在满足条件的物品</summary>

${job:player \*check-item \***{name(名字)} \*{amount(数量)}** \***{true/false(是否清除)}**}

**返回:** true/false

</details>

<details>

<summary>判断玩家主手/副手物品是否条件</summary>

${job:player \*check-hand **\*{type(main(主)/off(负))}** \***{name(名字)} \*{amount(数量)}** \***{true/false(是否清除)}**}

**返回:** true/false

</details>

<details>

<summary>判断当前对象或对象所属工作组是否可见</summary>

${job:player \*visible \***{content/object}**}

**返回:** true/false

</details>
