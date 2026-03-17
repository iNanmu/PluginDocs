# 洗练项目

## 前言

只有满足服务器已设洗练项目的物品可以进行洗练，可设置多个洗练项目

## 基础配置项

完整例子请查看 [Example.yml](xi-lian-xiang-mu.md#example.yml)

<table><thead><tr><th>配置项</th><th width="249.33333333333331">说明</th><th>例子</th></tr></thead><tbody><tr><td>name</td><td>洗练物品名要求 (模糊匹配)</td><td>name: <strong>"楠木的内裤"</strong></td></tr><tr><td>rows</td><td>每次洗练的词条数量 (可随机)</td><td>rows: <strong>"3"</strong> 或 rows: <strong>"1~3"</strong></td></tr><tr><td>lock</td><td>是否允许锁定词条</td><td>lock: <strong>true</strong></td></tr><tr><td>ceiling</td><td>洗练满 <strong>N</strong> 次后无法继续洗练</td><td>ceiling: <strong>10</strong></td></tr><tr><td>chance</td><td>洗练成功的几率</td><td>chance: <strong>100</strong></td></tr><tr><td>view-id</td><td>洗练界面限制</td><td>view: <strong>example</strong></td></tr><tr><td>refine-fixed-lore</td><td>洗练固定描述生成</td><td><pre class="language-yaml"><code class="lang-yaml">#每次洗练后将出现在洗练属性下方的描述
#支持变量 &#x26; 洗练变量
refine-fixed-lore:
  - "&#x26;f&#x26;m&#x26;l------------------------"
  - "&#x26;6上次洗练玩家: &#x26;f%player_name%"
  - "&#x26;6当前洗练次数: &#x26;f{refine-number}"
</code></pre></td></tr><tr><td>allowed-uses</td><td>允许使用的洗练道具类型/道具物品名</td><td><pre class="language-yaml"><code class="lang-yaml">#可使用的道具 (支持道具类型或道具名)
allowed-uses:
  #失败保护道具 (类型判断)
  - "aegis"
  #成功概率提升的道具 (类型判断)
  - "chance-upgrade"
  #道具物品名 (物品名判断)
  - "楠木的洗衣液"
</code></pre></td></tr><tr><td>permissions</td><td>玩家权限洗练强度加成</td><td><pre class="language-yaml"><code class="lang-yaml">permissions:
  "幸运儿": 10.0
</code></pre></td></tr><tr><td>commands</td><td>洗练完毕后执行命令</td><td><pre class="language-yaml"><code class="lang-yaml">#洗练完毕后执行命令
#玩家以 OP 权限执行 {player} 为玩家名
commands:
  - "eco take {player} 1000"
</code></pre></td></tr><tr><td>material</td><td>洗练材料配置 (<a href="xi-lian-xiang-mu.md#zi-ding-yi-gong-shi">公式计算</a>)</td><td><pre class="language-yaml"><code class="lang-yaml">#材料判断物品名,数量通过公式计算
material:
  - 洗练石: "5+({lock-number}*2)"
    增幅石: "5+({lock-number}*2)"
    楠木的内裤: "0+({lock-number}/3)"
</code></pre></td></tr><tr><td>attribute</td><td>洗练属性词条配置 (<a href="xi-lian-xiang-mu.md#zi-ding-yi-gong-shi">公式计算</a>)</td><td><a href="xi-lian-xiang-mu.md#shu-xing-ci-tiao-pei-zhi">详细</a></td></tr></tbody></table>

## 自定义公式&#x20;

洗练项目上所需材料、洗练属性词条的计算均可自定义公式，可使用提供的变量进行更灵活的属性值计算，同时支持 **PlaceholderAPI** 变量

| 占位符变量                | 说明                             |
| -------------------- | ------------------------------ |
| {refine-number}      | 物品洗练次数                         |
| {lock-number}        | 本次洗练锁定的词条数量                    |
| {permission-upgrade} | 权限额外强度加成                       |
| {addition-upgrade}   | 洗练道具(**addition-upgrade**) 的加成 |

## 属性词条配置

每个项目都可设置不限数量的词条，洗练时将在列表内随机抽取

```yaml
attribute:
  #节点可是任意文字，不可重复
  物理伤害:
    #最终属性条目 (可使用下方占位符变量)
    #{symbol} - 词条强度
    #{merge} - 合并值
    #{random} - 随机值
    #{max} - 计算公式后的最大值
    #{min} - 计算公式后的最小值
    - lore: "{symbol} 物理伤害 {random}"
      #最小值计算公式 (支持PlaceholderAPI变量计算)
      #格式 "基础值;公式" 最终将 基础值~公式值 进行随机
      min: "10;10+(10*{addition-upgrade}/100)+(0.5*{refine-number})"
      #最大值计算公式 (支持PlaceholderAPI变量计算)
      #格式 "基础值;公式" 最终将 基础值~公式值 进行随机
      max: "100;100+(100*{addition-upgrade}/100)+(0.5*{refine-number})"
      #合并值公式 (支持PlaceholderAPI变量计算)
      merge: "{random}+({random}*{addition-upgrade}/100)"
```

特殊配置项，以下特殊配置项均是加在 **洗练属性对应节点** 内，例如

```yaml
attribute:
  物理伤害:
    - lore: "{symbol} 物理伤害 {random}"
      min: "10;10+(10*{addition-upgrade}/100)+(0.5*{refine-number})"
      max: "100;100+(100*{addition-upgrade}/100)+(0.5*{refine-number})"
      merge: "{random}+({random}*{addition-upgrade}/100)"
      #洗练 >=10 次才可能出现该词条
      number: 10
      #洗练出该词条全服提醒
      remind: true
```

| 配置项    | 说明            | 例子         |
| ------ | ------------- | ---------- |
| number | 洗练次数要求        | number: 10 |
| remind | 洗练词条强度满足时全服提醒 | remind: 50 |
| only   | 洗练是否只出现一次该词条  | only: true |

## Example.yml

洗练项目配置位于 **./project** 文件夹中

```yaml
#项目物品
name: "楠木的内裤"
#洗练行数 (可以是随机条数)
#rows: "3"
rows: "1~3"
#是否允许锁定词条
lock: true
#洗练成功概率
chance: 100

#可使用的道具 (支持道具类型或道具名)
allowed-uses:
  #失败保护道具 (类型判断)
  - aegis
  #成功概率提升的道具 (类型判断)
  - chance-upgrade
  #道具物品名 (物品名判断)
  - 楠木的洗衣液

#权限强度加成
permissions:
  "幸运儿": 10.0

#洗练完毕后执行命令
#玩家以 OP 权限执行 {player} 为玩家名
commands:
  - "eco take {player} 1000"

#材料判断物品名,所需数量根据公式决定 (支持PlaceholderAPI变量计算)
#{refine-number} - 物品洗练次数
#{lock-number} - 锁定词条的数量
#{permission-upgrade} - 权限额外强度加成
material:
  - 洗练石: "5+({lock-number}*2)"
    增幅石: "5+({lock-number}*2)"
    楠木的内裤: "0+({lock-number}/3)"

#洗练属性公式 (支持PlaceholderAPI变量计算)
#{addition-upgrade}  - 材料额外强度
#{permission-upgrade} - 权限额外强度加成
#{refine-number} - 物品洗练次数
#{lock-number} - 锁定词条的数量
#{max} - 属性最大值 (公式计算后)
#{min} - 属性最小值 (公式计算后)
#{random} - 最小值~最大值随机
attribute:
  物理伤害:
    #最终属性条目
    #{symbol} - 词条强度
    #{merge} - 合并值
    #{random} - 随机值
    #{max} - 计算公式后的最大值
    #{min} - 计算公式后的最小值
    - lore: "{symbol} 物理伤害 {random}"
      #最小值计算公式 (支持PlaceholderAPI变量计算)
      #格式 "基础值;公式" 最终将 基础值~公式值 进行随机
      min: "10;10+(10*{addition-upgrade}/100)+(0.5*{refine-number})"
      #最大值计算公式 (支持PlaceholderAPI变量计算)
      #格式 "基础值;公式" 最终将 基础值~公式值 进行随机
      max: "100;100+(100*{addition-upgrade}/100)+(0.5*{refine-number})"
      #合并值公式 (支持PlaceholderAPI变量计算)
      merge: "{random}+({random}*{addition-upgrade}/100)"
  伤害加成:
    - lore: "{symbol} 伤害加成 +{random}"
      #洗练次数达到一定时出现
      number: 10
      #洗练词条强度大于设定时值触发全服提醒
      remind: 80
      #每次洗练是否只出现一次
      only: true
      min: "0.1;0.1+(0.1*{addition-upgrade}/100)+(0.05*{refine-number})"
      max: "1;1+(1*{addition-upgrade}/100)+(0.1*{refine-number})"
      merge: "{random}+({random}*{addition-upgrade}/100)"
```
