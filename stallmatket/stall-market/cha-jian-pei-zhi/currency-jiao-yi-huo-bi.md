# Currency (交易货币)

## 介绍

插件支持自定义交易货币，只需要你所需的货币来源于某个插件，而那个插件提供数值变量、数值增减操作命令即可自定义为一种货币

## 例子

根据下方例子及注释即可自由自定义新的建议货币，自定义货币后还需再 **config.yml** 配置内的优先级处设置对应的优先级数据 ( [config.yml](./#ji-chu-de-pei-zhi-config.yml) -> priority -> currency 配置项)

<pre class="language-yaml"><code class="lang-yaml">#货币名称
currency-name: "金币"
<strong>
</strong>#货币处理
currency-process:
    #判断玩家在购买商品时有没有足够的金币数量
  - condition: "%vault_eco_balance_fixed% >= {VALUE}"
    #不满足条件则提示该内容
    message: "&#x26;f你需要有 {VALUE} 金币"
    #满足后成功购买商品并执行该命令扣除玩家身上的金币
    commands:
      - "eco take %player_name% {VALUE}"

#货币储存 (通过摊位仓库储存货币)
currency-store:
    #判断玩家有没有足够的金币可以储存进仓库
  - condition: "%vault_eco_balance_fixed% >= {VALUE}"
    #不满足条件则提示该内容
    message: "&#x26;f你的金币只有 %vault_eco_balance_fixed%"
    #满足后将金币自动储存进仓库,并执行该命令扣除玩家身上的金币
    commands:
      - "eco take %player_name% {VALUE}"

#货币提取
#摊主出售完商品在摊位仓库内提取货币也是通过该功能
currency-extract:
  - message: "&#x26;f你的金币货币储存只有 {VALUE}"
    extract-message: "&#x26;f成功提取金币货币,数量 {VALUE}"
    #玩家通过摊位仓库提取货币时触发命令
    extracts:
      - "eco give %player_name% {VALUE}"

#摊主设置界面内显示的物品材质
#界面: stall_goods_sell.yml、stall_goods_purchase_price.yml
owner-item-meta:
  material: GOLD_INGOT
  name: "§f设置金币价格"
  lore:
    - "§f当前设置 §c{VALUE}"
    - " "
    - "§6SHIFT点击 §f重置设置"

#买家购买界面上显示物品 (商品为出售类型时)
#界面: player_buy.yml、player_sell_purchase.yml
buyer-item-meta:
  material: GOLD_INGOT
  name: "§f金币"
  lore:
    - "§f花费 §c{VALUE} §f购买"

#收购商品卖家(非摊主)界面上显示的物品 (商品为收购类型时)
#界面: player_sell_purchase.yml
seller-item-meta:
  material: GOLD_INGOT
  name: "§f金币"
  lore:
    - "§f收购价格 §c{VALUE} §f个"
    - " "
    - "§f摊主储存账户剩余 §c{STORE-VALUE} §f金币"
    - "§f小于 §c{VALUE} §f无法使用"

#摊位仓库货币储存显示
store-item-meta:
  material: GOLD_INGOT
  name: "§f金币"
  lore:
    - "§f当前储存数量 {VALUE}"
    - " "
    - "§6左键 §f储存货币"
    - "§6右键 §f提取货币"
</code></pre>
