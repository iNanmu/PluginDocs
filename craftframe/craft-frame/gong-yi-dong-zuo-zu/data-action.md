---
description: 数据动作
---

# Data Action

{% tabs %}
{% tab title="设置数据" %}
> 动作用法

```yaml
craft:data *key *set *内容 
```



> 动作作用

设置 `key` 上储存的数据为指定内容，可使用配套占位符 Data 进行读取
{% endtab %}

{% tab title="删除数据" %}
> 动作用法

```yaml
craft:data *key *remove 
```



> 动作作用

删除 `key` 上储存的数据
{% endtab %}

{% tab title="操作数值" %}
> 动作用法

```yaml
craft:data *key *add/take *数值(浮点类型)
```



> 动作作用

操作 `key` 上的数值增加或者扣除，当不存在时会自动创建改数据，可使用配套占位符 Data 读取
{% endtab %}
{% endtabs %}
