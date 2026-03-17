# Layout (界面布局)

## 介绍

在这里你可以修改插件所有界面的布局，任意修改，插件共有 15 个界面，可配合龙核、萌芽等插件覆盖

* main.yml (插件主界面)
* market.yml (摊位市场界面)
* market\_filter.yml (摊位市场筛选界面)
* player.yml (玩家打开摊位时的界面)
* player\_buy.yml (玩家购买摊位内商品时的界面)
* player\_item\_submit.yml (玩家购买摊位商品 **以物换物** 时的界面)
* player\_sell\_purchase.yml (玩家向摊位 **收购商品** 出售物品时的界面)
* stall.yml (摊主编辑摊位时显示的界面)
* stall\_list.yml (玩家查看自己摊位列表时的界面)
* stall\_goods\_sell.yml (摊主编辑摊位出售商品时的界面)
* stall\_goods\_purchase.yml (摊主编辑摊位收购商品时的设置界面)
* stall\_goods\_purchase\_price.yml (摊主编辑摊位收购商品收购价格时的界面)
* warehouse.yml (玩家查看摊位仓库时的界面)
* warehouse\_currency.yml (玩家查看货币仓库时的界面)
* warehouse\_item.yml (玩家从仓库提取物品时物品显示的界面)

## 布局物品动作介绍

动作及玩家在界面上点击物品时触发的效果，格式为以下

```yaml
  "F":
    material: FEATHER
    name: "§f摊位筛选"
    lore:
      - "§f支持对摊位物品、摊位数据"
      - "§f进行筛选并呈现"
    #动作KEY写在这里,不同KEY触发的效果不同
    #下方的 OPEN_FILTER 即点击后打开筛选界面
    action: "OPEN_FILTER"
```

<table><thead><tr><th width="261">KEY</th><th width="276">介绍</th><th>特别说明</th></tr></thead><tbody><tr><td>CREATE_STALL</td><td>创建摊位</td><td></td></tr><tr><td>CREATE_GOODS</td><td>创建摊位商品</td><td>在 stall.yml 界面使用</td></tr><tr><td>DELETE_GOODS</td><td>删除 所选摊位商品</td><td>仅可在商品编辑界面使用</td></tr><tr><td>STALL_ENTITY_OPERATION</td><td>摆放摊位操作</td><td>在 stall.yml 界面使用</td></tr><tr><td>RETURN_MAIN</td><td>返回/打开 插件主界面</td><td></td></tr><tr><td>RETURN_STALL_LIST</td><td>返回/打开 摊位列表界面</td><td></td></tr><tr><td>RETURN_STALL</td><td>返回 所选摊位界面</td><td></td></tr><tr><td>RETURN_GOODS</td><td>返回 所选商品编辑界面</td><td></td></tr><tr><td>RETURN_MARKET</td><td>返回/打开 摊位市场</td><td></td></tr><tr><td>RETURN_WAREHOUSE</td><td>返回/打开 摊位仓库界面</td><td></td></tr><tr><td>OPEN_CURRENCY_WAREHOUSE</td><td>打开 货币仓库界面</td><td></td></tr><tr><td>SELL_ITEM</td><td>出售商品时物品放置位</td><td>仅可在商品编辑界面使用</td></tr><tr><td>SET_PURCHASE_PRICE</td><td>设置收购商品收购价格</td><td>仅可在商品编辑界面使用</td></tr><tr><td>SET_PURCHASE_AMOUNT</td><td>设置收购商品收购数量</td><td>仅可在商品编辑界面使用</td></tr><tr><td>SET_BUY_AMOUNT</td><td>设置购买数量 (买家)</td><td>仅可在玩家购买界面使用</td></tr><tr><td>OPEN_FILTER</td><td>打开筛选界面</td><td></td></tr><tr><td>SWITCH_FILTER_STATE</td><td>切换筛选状态</td><td>即可在筛选界面使用</td></tr></tbody></table>

仅可在商品编辑界面使用&#x20;

> stall\_goods\_purchase.yml、stall\_goods\_purchase\_price.yml、stall\_goods\_sell.yml

仅可在玩家购买界面使用 :&#x20;

> player\_buy.yml

即可在筛选界面使用

> market\_filter.yml
