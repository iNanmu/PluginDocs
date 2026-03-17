# 洗练道具

## 前言

洗练物品时可放入不同类型的洗练道具，可以是 **保护符、成功几率提升道具、强度增幅道具** 等，一个完整的 洗练道具 示例配置

## 洗练道具配置

| 配置项   | 说明      | 例子                           |
| ----- | ------- | ---------------------------- |
| key   | 道具类型    | key: **chance-upgrade**      |
| data  | 道具效果值   | data: **10**                 |
| stack | 是否可叠加使用 | stack: **true ( 默认 false )** |

### 道具类型

<table><thead><tr><th>类型</th><th>说明</th><th>data 例子</th></tr></thead><tbody><tr><td>chance-upgrade</td><td>洗练几率提升</td><td>data: <strong>10</strong></td></tr><tr><td>addition-upgrade</td><td>洗练强度提升</td><td>data: <strong>10</strong></td></tr><tr><td>aegis</td><td>洗练失败保护 (防止物品破损)</td><td>data: <strong>true</strong></td></tr><tr><td>refine-number-reset</td><td>洗练次数重置</td><td>data: <strong>true</strong></td></tr><tr><td>insert-attribute</td><td>插入 <strong>属性或描述</strong></td><td><pre class="language-yaml"><code class="lang-yaml">  data:
    - "&#x26;4★ 暴击几率 +25%"
</code></pre></td></tr></tbody></table>

```yaml
洗练增幅符:
  key: addition-upgrade
  data: 10
  #叠加使用
  stack: true

暴击灵符:
  key: insert-attribute
  data:
    - "&4★ 暴击几率 +25%"
```

## Example.yml

洗练道具配置位于 **./props** 文件夹

```yaml
#物品名 (模糊匹配)
保护符:
  #类型
  key: aegis
  #数据值
  data: true

洗练成功符:
  key: chance-upgrade
  data: 10
  #是否可叠加使用
  stack: true

洗练增幅符:
  key: addition-upgrade
  data: 10
  #是否可叠加使用
  stack: true

暴击灵符:
  key: insert-attribute
  data:
    - "&4★ 暴击几率 +25%"
```
