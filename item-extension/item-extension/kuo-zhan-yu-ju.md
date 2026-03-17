---
description: Kether
---

# 扩展语句

## 说明

在插件 `条件、动作` 执行中支持使用 **Kether** 语句，同时插件自带部分 **ItemExtension** 私有语句

## 操作语句

相关用法可以查看 [扩展示例](kuo-zhan-shi-li/) 内的配置

| 语句                                        | 描述                         |
| ----------------------------------------- | -------------------------- |
| ie name array \[ 名称 ]                     | 修改装备名称                     |
| ie del-name array \[ true ]               | 恢复原始装备名称                   |
| ie itype array \[ 物品类型 ]                  | 修改装备类型                     |
| ie del-itype array \[ true ]              | 恢复原始装备类型                   |
| ie enchant array \[ 附魔 等级 ]               | 增加装备附魔                     |
| ie del-enchant array \[ 附魔 ]              | 清除装备附魔                     |
| ie nbt array \[ "key=value" "..." ]       | 设置NBT标签数据                  |
| ie del-nbt array \[ "key" "key" ]         | 删除NBT标签数据                  |
| ie custom-module-data array \[ value ]    | 设置物品 CustomModuleData 值    |
| ie del-custom-module-data array \[ true ] | 恢复原始装备 CustomModuleData  值 |

## 技能语句

支持 SkillAPI MythicMobs Planners 等插件技能

| 语句                           | 描述                 |
| ---------------------------- | ------------------ |
| sk-skill {技能名}               | 触发 SkillAPI 插件技能   |
| mythic-skill {技能名} {伤害(1.0)} | 触发 MythicMobs 插件技能 |
| planner-skill {技能名} {等级(1)}  | 触发 Planners 插件技能   |

## 占位符

| 占位符                       | 介绍            |
| ------------------------- | ------------- |
| \{{ ie-props name \}}     | 获取扩展道具名       |
| \{{ ie-props id \}}       | 获取扩展道具ID      |
| \{{ ie-props level \}}    | 获取扩展道具等级      |
| \{{ ie-props show\}}      | 获取扩展道具嵌入后的显示名 |
| \{{ ie-props identity \}} | 获取扩展道具可放置的扩展位 |

| 占位符                                         | 描述                             |
| ------------------------------------------- | ------------------------------ |
| \{{ ie-item name \}}                        | 放入扩展界面的装备名                     |
| \{{ ie-item type \}}                        | 放入扩展界面的装备类型                    |
| \{{ ie-item amount \}}                      | 放入扩展界面的装备数量                    |
| \{{ ie-item custom-module-data \}}          | 放入扩展界面的装备 custom-module-data   |
| \{{ ie-item contains **name/lore/type** \}} | 模糊匹配对应数据 ( 返回 true 或 false 值 ) |

**ie-item contains** 占位符使用例子:

```yaml
#放置条件设置
condition:
  # ie-item contains {name/lore/type} array [ params ] 模糊匹配对应类型数据
  - check {{ ie-item contains lore array [ "§f装备类型 §6主武器" "§f装备类型 §6副武器" ] }} == 'true'
```

在扩展道具配置页面中添加以上放置条件配置，放入扩展的装备需包含 `"§f装备类型 §6主武器"` 或 `"§f装备类型 §6副武器"` 的 `lore` 描述才可放置对应的扩展道具，该占位符为模糊匹配且不过滤颜色代码
