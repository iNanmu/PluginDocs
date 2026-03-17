---
description: 任务插件
---

# Chemdah

## 说明

新增任务目标 **"frame object"**

### **条件**

| 条件名          | 示例                       | 作用                 |
| ------------ | ------------------------ | ------------------ |
| content:name | content:name: **测试工作组**  | 判断触发对象所属工作组        |
| object:name  | object:name: **测试对象**    | 判断触发对象当前显示名        |
| data         | data: **成长值=100;?=?;..** | 判断事件接收的数据 **(注1)** |

**注1 :**  通过 **job:script event chemdah {data}** 传过来的数据，可判断多个或单个，条件使用例如：

```yaml
    1:
      objective: frame object
      condition:
        content-name: 测试工作组
    2:
      objective: frame object
      condition:
        object-name: 史莱姆
    #job:script event chemdah 成长值=100;可回收=true
    3:
      objective: frame object
      condition:
        data: 成长值=100;可回收=true
```

### 条件变量

| 变量名          | 作用          |
| ------------ | ----------- |
| content:name | 获取触发对象所属工作组 |
| object:name  | 获取触发对象当前显示名 |
