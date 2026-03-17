---
description: 插件的主命令有 /frame、/job-frame
---

# 插件命令

<details>

<summary>Create / 生成对象命令</summary>

/frame create **\[content] \[type] \[lasting] \[location]**

必选参数: **\[content(工作组名)]、\[type(对象类型)]**

可选参数: **\[lasting(是否为持久对象,默认临时对象)]、\[location(生成位置,默认脚下)]**

使用例子: /frame create 矿物 ENTITY true

</details>

<details>

<summary>Delete / 删除对象命令</summary>

/frame delete **\[id/uuid]**

必选参数: **\[id/uuid(对象ID/UUID)]**

使用例子: /frame delete ea5e8f36-eefd-4699-ace9-7012b1e8f905

</details>

<details>

<summary>Object / 对象位置命令</summary>

/frame object **\[tp/move] id/uuid]**

必选参数: **\[tp(传送至对象位置)/move(移动至当前位置)] \[id/uuid(对象ID/UUID)]**

使用例子: /frame tp ea5e8f36-eefd-4699-ace9-7012b1e8f905

</details>

<details>

<summary>Content / 工作组命令</summary>

/frame content - 查看服务器工作组信息

使用例子: /frame content

</details>

<details>

<summary>Reload / 重载命令</summary>

/frame reload **\[content]**

可选参数: **\[content(工作组名)]]**

使用例子: /frame reload All

</details>
