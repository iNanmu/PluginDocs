---
description: 地牢插件
---

# DungeonPlus

## 说明

新增 **地牢脚本** 以及兼容工作对象触发 **地牢脚本处理**

### **地牢脚本**

该脚本所生成的工作对象均为 **非持久对象** 即 **地牢结束、服务器关闭** 后就会自动清除

<details>

<summary>Job-Object</summary>

$job-object{**content**=工作组;**type**=类型;**operation**=操作类型;**location**=X,Y,Z} @dungeon

**\[content]** 工作组名称,例如 "蓝水晶矿"&#x20;

**\[type]** 对象类型(ENTITY/BLOCK)

**\[operation]** 操作类型(CREATE/DELETE)

**\[location]** 生成位置(X,Y,Z)<br>

例 $job-object{content=蓝水晶矿;type=ENTITY;operation=create;location=1788,4,959} @dungeon

</details>

### 地牢脚本处理

因为 **JobFrame** 插件支持 **Kether** 脚本，所以只需要在工作步骤里面使用 **DungeonPlus** 提供的 **Kether** 脚本即可触发地牢脚本处理，具体请查看 [**Dungeon**](https://kether.tabooproject.org/list.html#Dungeon)

```yaml
condition: 
  - ...
condition-is-met:
  - dungeon message dungeon params "向地牢内所有玩家发送这条消息"
```
