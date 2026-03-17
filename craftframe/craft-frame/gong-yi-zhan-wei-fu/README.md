# 工艺占位符

## 介绍

制作工艺时可使用调用 **`工艺占位符`** 获取数据，你必须学会 `Data、Random、Material-Data、Material-Central` 占位符的运用，那样子你能作出更多玩法，不局限于 **`锻造、炼药、重铸`** 等玩法

## 多层工艺占位符

从 1.0.6 插件版本开始，支持多层占位符功能，低层占位符可以套用高层的占位符

即每多一层 { } 即为更高一层的占位符，默认开启两层支持，如果需要更高层，请修改对应工艺图纸内的 `placeholder-layer` 配置项，默认设置为 2 即两层

拿 [Random](random.md) 占位符来做一个使用例子:

`{random *r:`<mark style="color:red;">`{`</mark>`random *r:1-10`<mark style="color:red;">`}`</mark>`-`<mark style="color:red;">`{`</mark>`random *r:10-100`<mark style="color:red;">`}`</mark>`}` 不能运行

`{random *r:`<mark style="color:red;">`{{`</mark>`random *r:1-10`<mark style="color:red;">`}}`</mark>`-`<mark style="color:red;">`{{`</mark>`random *r:10-100`<mark style="color:red;">`}}`</mark>`}` 可以运行

**总结** 只有低层可以套高层，高层不能套低层的占位符，越高层的占位符越先触发

## 全局计算占位符

这个占位符可以在配置的大部分地方所有，动作行、描述行、都可以使用，计算公式内可套占位符

格式为 `$[计算公式 *类型]` 类型有 `INT整数 DOUBLE浮点` 两种类型

使用例子 1  `$[1+1 *DOUBLE]` 返回的会是 2.0 如果将类型改为 INT 返回的将是 2&#x20;

使用例子 2 `$[1+{randon *r:1-10} *INT]` 返回的计算值会是 1+(随机1\~10) 所以支持占位符运算
