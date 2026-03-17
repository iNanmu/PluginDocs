---
description: 自定义摊位等级
---

# 摊位等级

## 介绍

玩家不同摊位之间的摊位等级互不干扰，每个摊位都有自己的等级数据，可设置多个摊位等级，每个摊位等级可设置不同的 税率、商品上架数量、摊位显示名、摊位实体类型

```yaml
#摊位等级
level:
  #摊位默认1级
  1:
    #所需经验
    exp: 0
    #每出售一件商品增加多少摊位经验
    #提取出售货物时获得
    sell-exp: 1
    #摊位选项
    options:
      #摊位实体类型
      type: VILLAGER
      #摊位实体名称
      name: "{STALL-OWNER} 的初级摊位"
      #摊位商品数量上限
      goods-size: 16
      #货币税收 (百分比)
      currency-tax:
        #货币配置文件名
        money: 16
        points: 16
  2:
    exp: 128
    sell-exp: 2
    options:
      type: VILLAGER
      name: "{STALL-OWNER} 的高级摊位"
      goods-size: 64
      currency-tax:
        money: 8
        points: 8
```

## 摊位模型

摊位模型目前仅支持类似 龙核、萌芽 那种根据实体名称替换模型的插件，你只需要自定义不同等级的摊位上的显示名即可做到不同等级显示不同模型，效果如下 ( **购买插件即送对应模型及配置** )

未来将根据需求支持其他形式的模型替换 (如NBT等)

<figure><img src="../../.gitbook/assets/}8OK8~K&#x60;FK{~O0FW&#x60;1%$RLB.png" alt=""><figcaption></figcaption></figure>
