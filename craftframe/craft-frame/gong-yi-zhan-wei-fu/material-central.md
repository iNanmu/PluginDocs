---
description: 工艺材料数据中控 占位符
---

# Material-Central

{% hint style="info" %}
该占位符与 **Material-Data** 占位符用法相同，唯一区别是不需要指定 **材料数据储存KEY** 该占位符的数据匹配及读取均为所有放入的材料
{% endhint %}

{% tabs %}
{% tab title="类型判断" %}
> 占位符格式

```yaml
{material-central *type *物品类型 *排除材料KEY(可选)}
```



> 占位符用法

获取工艺制作界面内放入的所有材料内是否存在类型匹配的项目

返回 **true / false**
{% endtab %}

{% tab title="名称/描述匹配" %}
> 占位符格式

```yaml
{material-central *contains *[文本,文本,...] *排除材料KEY(可选)}
```



> 占位符用法

获取工艺制作界面内放入的所有材料是否存在名称、描述匹配的项目，该匹配为模糊匹配

返回 **true / false**
{% endtab %}

{% tab title="名称匹配" %}
> 占位符格式

```yaml
{material-central *name-contains *[文本,文本,...] *排除材料KEY(可选)}
```



> 占位符用法

获取工艺制作界面内放入的所有材料是否存在描述匹配的项目，该匹配为模糊匹配

返回 **true / false**
{% endtab %}

{% tab title="描述匹配" %}
> 占位符格式

```yaml
{material-central *lore-contains *[文本,文本,...] *排除材料KEY(可选)}
```



> 占位符用法

获取工艺制作界面内放入的所有材料名称是否存在匹配的项目，该匹配为模糊匹配

返回 **true / false**
{% endtab %}

{% tab title="获取物品数量" %}
> 占位符格式

统计所有材料位上材料名包含指定字符的材料物品数量

<pre class="language-yaml"><code class="lang-yaml"><strong>{material-central *name-contains-size *[文本,文本,...] *排除材料KEY(可选)}
</strong></code></pre>

统计所有材料位上包含指定描述的材料物品数量

<pre class="language-yaml"><code class="lang-yaml"><strong>{material-central *lore-contains-size *[文本,文本,...] *排除材料KEY(可选)}
</strong></code></pre>



> 占位符用法

获取工艺制作界面内放入的所有材料的物品数量

返回 **符合条件的合计数量**
{% endtab %}
{% endtabs %}

{% tabs %}
{% tab title="描述筛选" %}
> 占位符格式

```yaml
{material-central *lore-filter *[文本,文本,...] *排除材料KEY(可选)}
```



> 占位符用法

获取工艺制作界面内放入的所有材料内包含指定文本的描述，该匹配为模糊匹配

返回 **符合的描述** 格式为 `"描述,描述,..."`
{% endtab %}

{% tab title="特殊格式 描述筛选" %}
> 占位符格式

```yaml
{material-central *plugin-lore-filter *[文本,文本,...]}
```



> 占位符用法

获取工艺制作界面内放入的所有材料内包含指定文本的描述，该匹配为模糊匹配

返回 **符合的描述** 格式为 `"$=[描述,描述,...]"` 多行格式<br>

{% hint style="info" %}
该占位符所返回的数据可使用 describe action 内的 add-line 方法，将筛选的描述复制到工艺制作物上
{% endhint %}
{% endtab %}
{% endtabs %}

{% tabs %}
{% tab title="标签读取 (数值)" %}
> 占位符格式

```yaml
{material-central *lore-value *读取格式 *排除材料KEY(可选)}
```



> 占位符用法

获取工艺制作界面内放入的所有材料内符合读取格式的数据值，该匹配为模糊匹配

返回 **数值 (浮点类型)**<br>

{% hint style="info" %}
格式例子 **"+(.\*?)% 锻造强度"** 即可读取指定材料数据储存数据描述上的  **(.\*?)** 上的数据值，也可以是 **"锻造强度 +(.\*?)"** 的格式，可完全自定义，读取出来的数值会乘以放入的材料数量
{% endhint %}
{% endtab %}
{% endtabs %}
