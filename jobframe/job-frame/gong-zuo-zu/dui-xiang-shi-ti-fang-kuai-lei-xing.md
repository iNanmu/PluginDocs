---
description: 文档无法访问的话挂个梯子
---

# 对象实体&方块类型

## Entity

该文档内部分类型无法使用，但原版基础生物类型都可以使用，如 **ZOMBIE、SLIME、PIG** 等，遇到不能用就换一个类型吧

```yaml
#实体对象设置
basic-entity:
    #史莱姆实体碰撞箱大小 (仅为史莱姆时可使用)
  - entity-collision-size: 1
    #实体类型
    entity-type: "SLIME"
    #默认实体对象显示名(可配合萌芽、龙核实体模型)
    default-name: "蓝水晶矿根"
```

{% embed url="https://jd.ptms.ink/adyeshach/-adyeshach/ink.ptms.adyeshach.common.entity/-entity-types/index.html" %}
实体类型
{% endembed %}

## Block

该文档内部分类型无法使用，那就换一个类型吧&#x20;

```yaml
#方块对象设置
basic-block:
    #方块类型
  - type: CREEPER_HEAD
    default-name: "蓝水晶矿根"
    #头颅数据 (可配合萌芽方块,龙之方块)
    default-skull-name: "model:grass"
```

{% embed url="https://github.com/TabooLib/taboolib/blob/master/platform/platform-bukkit/src/main/java/taboolib/library/xseries/XMaterial.java" %}
