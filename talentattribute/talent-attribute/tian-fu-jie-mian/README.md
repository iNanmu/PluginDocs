# 天赋界面

## 介绍

每个天赋界面都可以设置不同的 **天赋页(自定义布局)、天赋数据** 等内容，每个天赋界面都有唯一的KEY即 **page-name** ,用于储存数据,下面会讲到

## 天赋界面配置分布介绍

每个 **page-name** 必须是唯一的,整个服务器内没有重复的

```yaml
#天赋界面唯一KEY(用于储存数据)
page-name: "普通天赋页"

#天赋界面名 (这里面的 {page} 会替换成玩家打开的对应页数)
title: "属性天赋 {page}/2"

#天赋界面内不同页面布局 (使用界面布局物品占位符快速设置)
pages: ..

#天赋界面布局物品可调用的物品
materials: ...

#该天赋界面内的天赋数据配置
talents: ...
```

## 完整的配置例子

插件加载时会默认生成该配置内容，可在服务器内输入 **/talent open 你的名字 普通天赋页** 进行打开

```yaml
#天赋界面唯一KEY(用于储存数据)
page-name: "普通天赋页"
#界面名
title: "属性天赋 {page}/2"
#页面布局 (使用界面布局物品占位符快速设置)
pages:
  1:
    #打开界面时判断条件
    condition:
      - 'check %player_level% >= 100#&f你需要等级达到 &c100 &f级才可打开第一页天赋'
    #页面布局
    layout:
      - "####P####"
      - "####N####"
  2:
    condition:
      - 'check %talent_level_普通天赋页_力量天赋% >= 20#&f你需要将 &6力量天赋 &f升至 &c20 &f级才可打开第二页天赋'
      - 'check %player_level% >= 200#&f你需要等级达到 &c200 &f级才可打开第二页天赋'
    layout:
      - "####B####"
      - "##L###N##"

#界面布局物品
materials:
  #占位符
  N:
    #物品名
    - name: "&3下一页"
      #方法类型 NEXT / LAST / TALENT
      method: "next"
      #物品类型
      #https://github.com/TabooLib/taboolib/blob/master/platform/platform-bukkit/src/main/java/taboolib/library/xseries/XMaterial.java
      type: "PAPER"
      auto-update: true
      #物品介绍
      info:
        - "&f点击下一页"
        - "&f当前剩余 &c%talent_point_天赋点% &f点天赋点"
  L:
    - name: "&3上一页"
      method: "last"
      type: "PAPER"
      auto-update: true
      info:
        - "&f点击上一页"
        - "&f当前剩余 &c%talent_point_天赋点% &f点天赋点"
  P:
    - name: "&6力量天赋"
      type: "BLUE_STAINED_GLASS_PANE"
      method: "talent"
      #当 method 为 TALENT 时需要将对应天赋KEY填入以下参数
      talent: "力量天赋"
      #当 method 为 TALENT 时可使用 {talent-level} / {talent-attribute} 占位符
      #读取玩家对应的天赋数据,同时可以使用对应天赋KEY配置内的 formula 数据
      info:
        - "&f当前天赋等级: &c{talent-level}"
        - " "
        - "&f造成伤害就额外增加 &c{0} - {1}"
        - "&f点伤害并,永久增加自身 &c{2} &f点"
        - "&f物理防御"
        - " "
        - "&6SHIFT+右键 &f洗点返还 &c{5} &f点天赋点"
  B:
    - name: "&6嗜血天赋"
      type: "RED_STAINED_GLASS_PANE"
      method: "talent"
      talent: "嗜血天赋"
      info:
        - "&f当前天赋等级: &c{talent-level}"
        - " "
        - "&f当前将有 &c{0}% &f几率触发嗜血技能"
        - "&f对目标造成 &c{1}% &f点伤害并转换为"
        - "&f自身&a生命力"

talents:
  #可通过变量 %talent_level_普通天赋页_嗜血天赋% 读取玩家该天赋等级
  #可通过变量 %talent_point_普通天赋页_嗜血天赋% 读取玩家升级该天赋所消耗的天赋点
  #天赋KEY (同天赋界面组内不能相同)
  "嗜血天赋":
    #公式计算(计算后可在后面配置节点内取出,按 {0} ~ {N} 顺序)
    - formula:
        - "{v}*0.3"
        - "{v}*0.8"
        - "1+({v}/5)"
        - "{v}"
      #此次升级消耗天赋点点数
      demand: "{2}"
      demand-type: "天赋点"
      #此次升级天赋条件
      condition:
        - 'check {3} <= 30#&6嗜血天赋 &f已达到天赋等级上限'
        - 'check %player_level% >= {2}#你需要达到 {2} 级才可升级天赋'
      #天赋属性加成
      attribute:
        - "  &f吸血几率: &c{0}"
        - "  &f吸血倍率: &c{1}"
  #天赋KEY (同天赋界面组内不能相同)
  "力量天赋":
    #公式计算(计算后可在后面配置节点内取出,按 {0} ~ {N} 顺序)
    - formula:
        - "{v}*0.5"
        - "{v}*0.8"
        - "{v}*5"
        - "1+({v}/5)"
        - "{v}"
        #此计算用于洗点返回 80% 的天赋点
        - "%talent_point_普通天赋页_力量天赋%*0.8"
      #此次升级消耗天赋点点数
      demand: "{3}"
      demand-type: "天赋点"
      #此次升级天赋条件
      condition:
        - 'check {4} <= 50#&6力量天赋 &f已达到天赋等级上限'
        - 'check %player_level% >= {2}#你需要达到 {2} 级才可升级天赋'
      #天赋属性加成
      attribute:
        - "  &f物理伤害: &c{0} - {1}"
        - "  &f物理防御: &c{0}"
      #是否允许洗点
      wash: true
      #洗点条件
      wash-condition:
        - 'check {4} >= 50#&f需要 &6力量天赋 &f达到 &c50 &f级后才可洗点'
      #洗点后触发命令 (满足条件后)
      wash-command:
        - 'talent point give %player_name% {5} 天赋点'
```
