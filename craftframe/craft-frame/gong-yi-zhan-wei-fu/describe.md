---
description: 描述组占位符
---

# Describe

{% tabs %}
{% tab title="描述组随机" %}
> 占位符格式

```yaml
{describe *random-lines *工艺描述组 *随机行数 *是否重复(true/false)}
```



> 占位符用法

指定工艺图纸预设的 **描述组** 进行随机，可指定随机行数、是否随机出重复描述行

返回格式 `"内容,内容"` 格式
{% endtab %}

{% tab title="特殊格式 描述组随机" %}
> 占位符格式

```yaml
{describe *random-special-lines *工艺描述组 *随机行数 *是否重复(true/false)}
```



> 占位符用法

指定工艺图纸预设的 **描述组** 进行随机，可指定随机行数、是否随机出重复描述行

返回格式 `"$=[内容,内容]"` 该格式为多行格式
{% endtab %}

{% tab title="获取起始行至结束行的行数" %}
> 占位符格式

```yaml
{describe *get-part-line-size *起始行(非模糊匹配) *结束行(非模糊匹配)}
```



> 占位符用法

获取工艺制作物描述从 `起始行` 至 `结束行` 内的描述行数

返回格式 `行数`
{% endtab %}
{% endtabs %}

