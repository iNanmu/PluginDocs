---
description: 描述动作
---

# Describe Action

1.0.1 更新 **描述组随机** 方法

{% tabs %}
{% tab title="使用描述组" %}
> 动作用法

```yaml
craft:describe *add *工艺描述组
```



> 动作作用

为工艺制作物增加上 `工艺描述组` 组内的描述 `工艺描述组` 是自定义在工艺图纸配置内的数据，这边可以看 **工艺图纸** 介绍页面，上的 [工艺描述组](../gong-yi-tu-zhi-zhu-pei-zhi/#gong-yi-miao-shu-zu)
{% endtab %}

{% tab title="描述组随机" %}
> 动作用法

<pre class="language-yaml"><code class="lang-yaml"><strong>craft:describe *random-line *工艺描述组 *随机行数 *是否可随机出重复(true/false)
</strong></code></pre>



> 动作作用

为工艺制作物增加上 `工艺描述组` 组内随机行数，同时可设置是否出现重复，`工艺描述组` 是自定义在工艺图纸配置内的数据，这边可以看 **工艺图纸** 介绍页面，上的 [工艺描述组](../gong-yi-tu-zhi-zhu-pei-zhi/#gong-yi-miao-shu-zu)
{% endtab %}

{% tab title="新增描述行" %}
> 动作用法

```yaml
craft:describe *add-line *文本  #单行格式
```

```yaml
craft:describe *add-line *$=[文本,文本,...]  #多行格式
```



> 动作作用

为工艺物增加一行、多行描述
{% endtab %}

{% tab title="删除描述行" %}
> 动作用法

```yaml
craft:describe *remove *文本(模糊匹配)
```



> 动作作用

模糊匹配删除工艺物上已设置的描述
{% endtab %}
{% endtabs %}

{% tabs %}
{% tab title="隐藏" %}
复制材料数据太长，隐藏下自己点上面切换
{% endtab %}

{% tab title="复制材料数据" %}
> 动作用法

```yaml
craft:describe *copy-material *工艺材料数据KEY
```



> 动作作用

复制玩家放入工艺制作界面内的材料数据，包括 **物品名、描述、类型、数量、NBT** 数据，这个东西再重铸例子上使用了，有疑问可以去看看，如果不知道数据KEY不知道是什么请看图

<figure><img src="../../../.gitbook/assets/0W]0U4P%S7]9%YP@LM7DKXQ.png" alt=""><figcaption><p>KEY</p></figcaption></figure>
{% endtab %}
{% endtabs %}

## 基础替换操作

{% tabs %}
{% tab title="替换描述组" %}
> 动作用法

```yaml
craft:describe *replace-group *文本(模糊匹配) *工艺描述组 *替换次数(超过次数的不替换/可选参数)
```



> 动作作用

模糊匹配工艺物上的描述并替换为工艺描述组内的内容，多行替换，这边可以看 **工艺图纸** 介绍页面，上的 [工艺描述组](../gong-yi-tu-zhi-zhu-pei-zhi/#gong-yi-miao-shu-zu)
{% endtab %}

{% tab title="替换描述行" %}
> 动作用法

```yaml
craft:describe *replace *文本(模糊匹配) *替换行(可使用多行格式) *替换次数(超过次数的不替换/可选参数)
```



> 动作作用

模糊匹配工艺物上的描述，将那行替换为指定 **描述**(可使用 `"$=[内容,内容]"` 多行格式) 该动作脚本会多行匹配并替换
{% endtab %}

{% tab title="替换描述文本" %}
> 动作用法

```yaml
craft:describe *replace-text *文本 *替换为文本
```



> 动作作用

模糊匹配工艺物上存在指定文本的描述，将描述上的文本替换为指定文本
{% endtab %}
{% endtabs %}

## 数值计算替换操作

{% tabs %}
{% tab title="计算并替换" %}
> 动作用法

<pre class="language-yaml"><code class="lang-yaml"><strong>craft:describe *replace-value *描述(模糊匹配) *计算公式(@value为描述上获取的数值)
</strong></code></pre>



> 动作作用

模糊匹配工艺物上的描述并对描述进行取值(**@value**)，后通过 **计算公式计算后重新替换** 到原先描述上，可配合改动作脚本做到词条强化功能

例如 `craft:describe *replace-value *物理伤害 *@value+10` 会将工艺物上包含 物理伤害 的描述的值进行提取，并通过 `@value+10` 的计算公式计算后替换回去，原 `物理伤害 +10` 会变成 `物理伤害 +20`
{% endtab %}

{% tab title="部分描述筛选计算并替换" %}
> 动作用法

<pre class="language-yaml"><code class="lang-yaml"><strong>craft:describe *replace-part-value *起始行 *结束行 *计算公式 *排除起始/结束行(true/false) *随机行数(可选)
</strong></code></pre>



> 动作作用

具体作用与 **计算并替换数值** 动作脚本相同，不同的是非匹配描述字符，而是匹配从 起始行至结束行 之间的描述，并可指定随机行数(可选)

该脚本典型的使用例子可在 [强化示例](../gong-yi-shi-li-pei-zhi/qiang-hua-shi-li.md) 上查看
{% endtab %}

{% tab title="部分描述筛选计算并替换-从组" %}
> 动作用法

<pre class="language-yaml"><code class="lang-yaml"><strong>craft:describe *replace-part-value-g *起始行 *结束行 *计算公式 *排除起始/结束行(true/false) *数据组 *随机行数(可选)
</strong></code></pre>



> 动作作用

具体作用与 **计算并替换数值** 动作脚本相同，不同的是非匹配描述字符，而是匹配从 起始行至结束行 之间的描述，并根据 **数据组(描述组)** 内配置的关键词及数值匹配，下面例子先看再用\
\
下面给个简单的使用示例，假设数据组为以下

```yaml
#没错,数据组就是在描述组内设置
describes:
  "数据组":
    #格式为 "关键词 set 数值"
    - "物理伤害 set 100"
    - "生命力 set $[{random rd:100.0-500.0}]"
```

物品属性为

```yaml
起始LORE
物理伤害: 10
生命力: 100
结束LORE
```

脚本为，这里面的 **@value** 是描述上匹配的值 **@group-value** 是数据组设置的值

```yaml
craft:describe *replace-part-value-g *起始LORE *结束LORE  *@value+@group-value *true
```

脚本触发后的效果会是

```yaml
起始LORE
物理伤害: 10 -> 110
生命力: 100 -> 100+(100.0~500.0)
结束LORE
```
{% endtab %}
{% endtabs %}



## 筛选部分描述操作

1.0.1 更新 **筛选部分描述操作** 方法

1.0.5 更新 **插入描述** 方法

1.0.7 部分方法更新 `排除起始/结束行` 参数

{% tabs %}
{% tab title="删除部分描述" %}
> 动作用法

```yaml
craft:describe *remove-part *起始行 *结束行 *排除起始/结束行(false)
```

> 动作作用

起始行、结束行 均为精准匹配，非模糊匹配\
精准匹配工艺物描述将 `起始行` 至 `结束行` 内的描述删除，包括起始行、结束行

```yaml
例如 物品描述 如下
- "AAA"
- "起始A"
- "BBB"
- "结束B"

那么 [craft:describe *remove-part *起始A *结束B *false] 会删除一下这部分描述
- "起始A"
- "BBB"
- "结束B"
```
{% endtab %}

{% tab title="部分描述替换为描述组" %}
> 动作用法

```yaml
craft:describe *replace-part-group *起始行 *结束行 *描述组名(配置预设) *排除起始/结束行(false)
```

> 动作作用

起始行、结束行 均为精准匹配，非模糊匹配\
精准匹配工艺物描述将 `起始行` 至 `结束行` 内的描述替换为指定 `描述组` 内容，`描述组` 可以看 **工艺图纸** 介绍页面，上的 [工艺描述组](../gong-yi-tu-zhi-zhu-pei-zhi/#gong-yi-miao-shu-zu)
{% endtab %}

{% tab title="部分描述替换文本" %}
> 动作用法

```yaml
craft:describe *replace-part-line *起始行 *结束行 *文本 *排除起始/结束行(false)
```

```yaml
craft:describe *replace-part-line *起始行 *结束行 *$=[多行格式] *排除起始/结束行(false)
```

> 动作作用

起始行、结束行 均为精准匹配，非模糊匹配\
精准匹配工艺物描述将 `起始行` 至 `结束行` 内的描述替换为指定的 `单行或多行` 文本，典型的使用例子是 [继承示例](../gong-yi-shi-li-pei-zhi/ji-cheng-shi-li.md) 配置
{% endtab %}

{% tab title="插入描述" %}
#### 1.0.5 更新-插入描述方法

> 动作用法

```yaml
craft:describe *insert-part-line *起始行 *结束行 *描述(可使用多行格式)
```

> 动作作用

起始行、结束行 均为精准匹配，非模糊匹配\
精准匹配工艺物描述在 `起始行` 至 `结束行` 的描述之间插入描述，可使用 `$=[内容,内容]` 多行格式，插入多行
{% endtab %}
{% endtabs %}

{% tabs %}
{% tab title="替换部分描述中指定行" %}
> 动作用法

```yaml
craft:describe *replace-part-index-line *起始行 *结束行 *行数 *内容
```

> 动作作用

取出 `起始行` 至 `结束行` 部分内的描述，并将指定行数上的描述替换为 <mark style="color:orange;">`指定内容`</mark>

行数也可以使用占位符 <mark style="color:orange;">`T=第一行`</mark> <mark style="color:orange;">`B=最后一行`</mark> <mark style="color:orange;">`B-=最后第二行`</mark>

```yaml
例如 物品描述 如下
- "起始A"
- "AAA"
- "BBB"
- "CCC"
- "结束B"

[craft:describe *replace-part-index-line *起始A *结束B *B *测试测试] 效果:
- "起始A"
- "AAA"
- "BBB"
- "测试测试"
- "结束B"

[craft:describe *replace-part-index-line *起始A *结束B *2 *测试测试] 效果:
- "起始A"
- "AAA"
- "测试测试"
- "CCC"
- "结束B"
```
{% endtab %}
{% endtabs %}
