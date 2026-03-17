---
description: 工艺图纸占位符
---

# Content

{% tabs %}
{% tab title="获取阶段总数" %}
> 占位符格式

```yaml
{content *phase-size}
```



> 占位符用法

获取当前制作的工艺图纸 **制作阶段总数**
{% endtab %}

{% tab title="获取当前阶段" %}
> 占位符格式

```yaml
{content *current-phase-size}
```



> 占位符用法

获取当前制作的工艺图纸的 **当前制作的阶段**
{% endtab %}

{% tab title="获取阶段制作时长" %}
> 占位符格式

```yaml
{content *current-phase-time}
```



> 占位符用法

获取当前制作的工艺图纸的 **当前制作阶段所需时长**
{% endtab %}
{% endtabs %}

{% tabs %}
{% tab title="完成时间" %}
> 占位符格式

```yaml
{content *run-phase-time}
```



> 占位符用法

获取当前制作的工艺图纸 正在制作的阶段完成时间 ( 格式 yyyy-MM-dd/HH:mm:ss )
{% endtab %}

{% tab title="工艺等级" %}
> 占位符格式

```yaml
{content *level}
```



> 占位符用法

获取玩家对当前制作的工艺图纸的 **学习等级**
{% endtab %}

{% tab title="工艺熟练度" %}
> 占位符格式

```yaml
{content *proficiency}
```



> 占位符用法

获取玩家对当前制作的工艺图纸的 **熟练度**
{% endtab %}
{% endtabs %}
