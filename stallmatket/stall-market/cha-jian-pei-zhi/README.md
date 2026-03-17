# 插件配置

## 说明

插件配置文件夹共分为四个配置文件夹

* currency (交易货币)
* lang (语言文件)
* layout (界面布局)
* material (界面基础布局材料)&#x20;

#### 基础的配置 (CONFIG.YML)

建议仔细阅读，部分功能Wiki页面无介绍

```yaml
#请将授权码填至此处
code: "插件授权码"

#储存设置
sql:
  #关闭则将数据储存至本地
  enable: false
  host: localhost
  port: 3306
  user: root
  password: asd123123
  database: smarker

#其他选项
options:
  #数据同步 (多服之间需要开启)
  #用于多服之间商品数据同步,摊位数据同步
  #修改该项配置需要重启服务器生效
  - database-sync: false
    #摊位对象类型
    stall-entity-type: VILLAGER
    #摊位对象默认名
    stall-entity-name: "{STALL-OWNER} 的摊位"
    #摊位商品物品名上架限制 (模糊匹配)
    stall-item-name-limit:
      - "禁止上架"
    #摊位商品描述上架限制 (模糊匹配)
    stall-item-lore-limit:
      - "禁止上架"
      - "已绑定"
    #每个玩家默认可创建多少个摊位
    stall-default-amount: 3
    #摊位权限,格式 权限#额外摊位数量#额外摊位商品数量上限
    #通过给予玩家 stall.<权限名> 即可额外增加摊位、商品数量上限
    stall-permissions:
      #以这个为例只需将 stall.vip 权限给予玩家
      - "vip#3#3"
    #GeekMail邮箱插件兼容
    #启动后摊位卖出商品后会发送邮件提示摊主
    geek-mail: false

#摆摊区域限制 (没有限制的世界则全图可放置)
area:
  - "world#100,50,100#150,100,150"

#摊位等级
level:
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


#优先级设置
#此处优先级影响界面显示顺序,处理顺序
priority:
  #交易货币
  #后期自定义的新货币也需配置对应的优先级
  currency:
    #以物换物
    custon-item: 1
    #金币货币
    money: 2
    #点券货币
    points: 3
  #筛选项
  filter:
    #摊位商品名筛选
    stall-goods-name-filter: 1
    #摊位商品描述筛选
    stall-goods-lore-filter: 2
    #摊位摊主黑名单筛选
    stall-owner-black-list-filter: 3
    #摊位货币价格区间筛选
    #后期自定义的新货币也需配置,格式如下
    #custom-currency-filter#货币配置名
    custom-currency-filter#money: 4
    custom-currency-filter#points: 5
  #收购项
  purchase:
    #收购物品名条件
    purchase-name: 1
    #收购描述条件 (收购的物品必须所设描述)
    purchase-lore: 2
    #收购可选描述条件 (收购的物品包含以下任意描述即可)
    purchase-optional-lore: 3
    #收购黑名单 (不收购某些玩家的物品)
    purchase-black-list: 4
```
