# 扩展示例

## 说明

你可以使用下面所提供的 **MythicMobs** 物品及技能配置，并结合提供的示例在服务器中实际使用一遍

这能使你加快对 **ItemExtension** 插件的学习

## 配置

**MythicMobs** 视频中使用的是 **4.7.2** 理论支持高版本，技能需要安装 **MythicMobsExtension** 插件

这里提供相关插件，请自行寻找下载地

\
物品配置

```yaml
星陨剑:
  Id: IRON_SWORD
  Display: '&6星陨剑'
  Lore:
  - ' &f装备类型: 主手'
  - ' '
  - ' &6◆ 装备属性'
  - '   &f物理伤害 &f+30'
  - '   &f暴击几率 &f+5'
  - '   &f暴击伤害 &f+30'
  - ' '
  - ' &b◆ 装备附§b魔'
  - '   &f[&7附魔&f] &f[&7附魔&f] &f[&7附魔&f]'
  - ' '
  - ' &e◆ 装备宝石'
  - '   &f[&7方形&f] &f[&7菱形&f] &f[&7方形&f] &f[&7菱形&f]'
  - ' '
  - ' &5◆ 星陨之力'
  - '§-   &f[&7空缺&f] 增加 &650% &f暴击伤害'
  - '§-   &f[&7空缺&f] 增加 &610% &f暴击几率'
  - '§-   &f[&7空缺&f] &610% &f概率触发 &5&l陨星 &f专属技能'
```



陨星技能配置

```
陨星:
  Cooldown: 0
  Skills:
  - sendtitle{title="&8♊&0&k &c&l陨星&0&k &8♊";d=80;fi=25;fo=25} @self
  - projectile{type=METEOR;g=0.1;onTick=陨星特效;onHit=陨星命中伤害;onEnd=陨星保底伤害;v=100;i=1;g=0.3;mr=60;hfs=30;hnp=true;hR=1.0;vR=1.0} @RLNTE{amount=10;radius=5;spacing=2;minradius=1}
陨星特效:
  Skills:
  - effect:particles{p=reddust;color=#8A2BE2;a=10;vS=0.5;hS=0.5} @Origin
  - effect:particles{p=flame;a=10;vS=0.5;hS=0.5} @Origin
  - effect:particles{p=largesmoke;a=5;vS=0.5;hS=0.5} @Origin
陨星命中伤害:
  Skills:
  - effect:sound{sound=random.explode;volume=2;p=1} @PIR{r=30}
  - effect:particles{particle=hugeexplosion;amount=10;vSpread=0.1;hSpread=0.1;Speed=1;yOffset=0}
  - effect:particles{particle=flame;amount=5;vSpread=1;hSpread=1;Speed=1;yOffset=0}
  - effect:particles{particle=smoke;amount=5;vSpread=2;hSpread=1;Speed=1;yOffset=0}
  - effect:particles{particle=lava;amount=5;vSpread=2;hSpread=1;Speed=1;yOffset=0}
  - effect:particles{particle=lava;amount=5;vSpread=3;hSpread=1;Speed=1;yOffset=0}
  - effect:particles{particle=reddust;amount=10;vSpread=3;hSpread=1;Speed=0.01;yOffset=0}
  - throw{velocity=6;velocityY=6} @LivingEntitiesInRadius{r=5}
  - potion{type=SLOW;duration=100;level=4} @LivingEntitiesInRadius{r=5}
  - damage{a=1;i=false} @LivingEntitiesInRadius{r=5}
陨星保底伤害:
  Skills:
  - damage{a=1} @LivingEntitiesInRadius{r=5}
```
