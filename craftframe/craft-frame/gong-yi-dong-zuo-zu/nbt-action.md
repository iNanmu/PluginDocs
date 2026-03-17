---
description: 类型动作
---

# Nbt Action

{% tabs %}
{% tab title="设置NBT数据" %}
> 动作用法

```yaml
craft:nbt *set *NBT名 *type *value
```

```yaml
craft:nbt *set *NBT名.NBT名 *type *value
```



> 动作作用

设置工艺物物品NBT数据值，参数内的 `type` 分别有 string、int、double、byte
{% endtab %}

{% tab title="删除NBT数据" %}
> 动作用法

```yaml
craft:nbt *remove *NBT名
```



> 动作作用

删除工艺物物品指定NBT数据
{% endtab %}
{% endtabs %}
