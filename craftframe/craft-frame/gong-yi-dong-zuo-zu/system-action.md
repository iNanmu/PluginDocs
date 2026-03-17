---
description: 工艺系统动作
---

# System Action

{% tabs %}
{% tab title="结束" %}
> 动作用法

```yaml
craft:system *stop
```



> 动作作用

结束此次工艺制作，不会打开工艺物提取界面 (直接结束)
{% endtab %}

{% tab title="结束并提取" %}
> 动作用法

```yaml
craft:system *extract-stop
```



> 动作作用

结束工艺制作并打开已制作的工艺物提取界面，当没有工艺物可提取时不开启提取界面

典型的使用例子是 重铸 你可以去看看 **EXAMPLE\_3.YML** 的配置例子
{% endtab %}

{% tab title="熟练度" %}
> 动作用法

```yaml
craft:system *proficiency *set/add/take *value
```



> 动作作用

操作玩家对该工艺图纸的熟练度
{% endtab %}

{% tab title="等级" %}
> 动作用法

```yaml
craft:system *level *set/add/take *value
```



> 动作作用

操作玩家对该工艺图纸的学习等级
{% endtab %}

{% tab title="触发自定义动作组" %}
> 动作用法

```yaml
craft:system *perform-actions *自定义动作组名 *执行次数(默认1)
```



> 动作作用

执行 `custom-actions` 配置项内设置的动作组，具体介绍请查看 [自定义动作组](../gong-yi-tu-zhi-zhu-pei-zhi/zi-ding-yi-dong-zuo-zu.md)
{% endtab %}
{% endtabs %}
