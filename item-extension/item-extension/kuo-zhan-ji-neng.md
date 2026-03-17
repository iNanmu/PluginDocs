# 扩展技能

## 说明

如果想要让你的扩展道具能够拥有技能效果，你就需要用到该功能

自定义后的扩展技能可在 **套装系统、扩展道具** 内使用，同时提供不同触发类型

## 触发器

<table><thead><tr><th>类型</th><th>描述</th><th><select><option value="ccb87aa3a81049419b89fe8f53e4f92a" label="释放目标为攻击到的实体" color="blue"></option><option value="ca3aa72ba8014673bc9b4aadf5bb6133" label="释放目标为攻击你的实体" color="blue"></option><option value="ae97c5e53bcd45adb8956bb6e1eaedf9" label="释放目标为被击杀的实体" color="blue"></option><option value="ed3431f834374477a47b5811f322e371" label="释放目标为击杀你的实体" color="blue"></option><option value="89a9fdbc8eb24db8a4889838e593fea0" label="释放目标为你右键的实体" color="blue"></option><option value="163237e54d1841e3b47fe60098ddf6a3" label="无释放目标" color="blue"></option></select></th></tr></thead><tbody><tr><td>ATTACK</td><td>攻击时触发</td><td><span data-option="ccb87aa3a81049419b89fe8f53e4f92a">释放目标为攻击到的实体</span></td></tr><tr><td>DEFENSE</td><td>防御时触发</td><td><span data-option="ccb87aa3a81049419b89fe8f53e4f92a">释放目标为攻击到的实体</span></td></tr><tr><td>RUNTIME</td><td>循环触发</td><td><span data-option="163237e54d1841e3b47fe60098ddf6a3">无释放目标</span></td></tr><tr><td>LEFT</td><td>左键时触发 (空气/方块)</td><td><span data-option="163237e54d1841e3b47fe60098ddf6a3">无释放目标</span></td></tr><tr><td>RIGHT</td><td>右键时触发 (空气/方块)</td><td><span data-option="163237e54d1841e3b47fe60098ddf6a3">无释放目标</span></td></tr><tr><td>RIGHT_ENTITY</td><td>右键实体时触发</td><td><span data-option="89a9fdbc8eb24db8a4889838e593fea0">释放目标为你右键的实体</span></td></tr><tr><td>RESPAWN</td><td>重生时触发</td><td><span data-option="163237e54d1841e3b47fe60098ddf6a3">无释放目标</span></td></tr><tr><td>DEATH</td><td>死亡时触发</td><td><span data-option="ed3431f834374477a47b5811f322e371">释放目标为击杀你的实体</span></td></tr><tr><td>KILL</td><td>击杀时触发</td><td><span data-option="ae97c5e53bcd45adb8956bb6e1eaedf9">释放目标为被击杀的实体</span></td></tr></tbody></table>

## 小知识

如果你需要判断玩家是否按住 **SHIFT+右键** 那么你可以使用 **RIGHT** 触发器并在技能触发条件中使用 **Kether** 提供的 `player sprinting` 语句，例如以下

```yaml
示例:
  type: "RIGHT"
  cooling: 10
  #触发条件
  action-conditions:
    #判断触发玩家是否为疾跑状态,模拟按下SHIFT效果
    - check player sprinting == true
  actions:
    - send '触发 SHIGT+右键 技能!'
```

更多 **Kether** 条件语句，可以查看 [官方文档](https://kether.tabooproject.org/list.html)

## 配置说明

该配置为 **装备赋能** 示例配置，你可以在 [扩展示例](kuo-zhan-shi-li/) 中找到相关配置

```yaml
#技能名
星陨技能:
  #触发类型
  type: "ATTACK"
  #是否唯一效果,默认为是
  #即多个装备拥有该技能的扩展道具时只触发一次
  only: true
  #冷却时间
  cooling: 10
  #触发条件
  action-conditions:
    #模拟概率
    - check random 100.0 >= 80.0
  actions:
    #使用 MythicMobs 插件技能
    #同时兼容 SkillAPI Planners 插件技能,详细查看 扩展语句 介绍
    - mythic-skill 陨星释放 1.0
    - send '§c§l星陨 §f技能进入 §610 §f秒冷却'
```

