---
description: JavaScript 条件判断，最为常用的判断脚本
---

# Js-Condition

## 脚本参数

标注 **\*** 为必填参数，带有 **\*N** 为支持 英文逗号隔开多个

| 参数          | 说明                                          |
| ----------- | ------------------------------------------- |
| text **\*** | JavaScript 表达式 **( 支持 PlaceholderAPI 变量 )** |
| message \*  | 不通过时全队提示                                    |

{% hint style="info" %}
当判断文本时应用 **' '** 符号包围判断文本，例如 **test == test** 不对，而是 **'test' == 'test'**
{% endhint %}

## 脚本类型

**all** 代表所有的脚本类型都支持

| 类型     | 说明           |
| ------ | ------------ |
| system | 判断地牢队伍内的所有玩家 |
| self   | 判断触发者        |

## 示例

```yaml
$js-condition{text=%player_level%>100;message=玩家 <player> 等级小于 100} @system
```
