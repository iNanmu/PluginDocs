---
description: 该功能从 1.0.8 版本开始
---

# 地牢占位符

## 地牢占位符是干什么的？

类似 **PlaceholderAPI** 的占位符功能，但不同的是 **PlaceholderAPI** 只能在 **部分脚本上使用** 而 **地牢占位符** 可以在每一行脚本上使用，例如 **\<mob:kill-amount \*小白>** 可以获取当前地牢内玩家已击杀小白怪物的数量，这是 **PlaceholderAPI** 无法做到的

## 地牢占位符格式

占位符的格式为 **<头:参数1 \*参数2 \*...>** 参数之间的间隔用 ' \*' 这个空格一定要加不可忽略

## @SELF 注意

一般支持 @SELF 类型的占位符，如果用 @SELF 通常数据来源于触发者自身，例如 [**Item**](https://ersha.gitbook.io/dungeonplus/di-lao/di-lao-zhan-wei-fu/item) 用 @SELF 时是检测触发者背包的物品，用 @SYSTEM 时是检测整个地牢内的玩家背包

## 开发者-怎么注册地牢占位符?

实现 **DungeonPlaceholder** 接口即可注册

```kotlin
interface DungeonPlaceholder : DungeonComponent {

    /**
     * 占位符头
     */
    val head: String

    /**
     * 所属插件
     */
    val plugin: String

    /**
     * 例子
     */
    val example: String

    /**
     * 支持的脚本类型列表,空则全部类型支持
     */
    fun getSupportType(): Array<ScriptType>? {
        return null
    }

    /**
     * [dungeon] 地牢对应地牢
     * [params] 参数,即 'hand:params' 某个 [ *值] 都为一参数值
     */
    fun onRequest(dungeon: Dungeon, params: Array<String>): String? {
        return null
    }

    /**
     * [dungeon] 地牢对应地牢
     * [params] 参数,即 'hand:params' 某个 [ *值] 都为一参数值
     * [trigger] 触发者
     */
    fun onRequest(dungeon: Dungeon, params: Array<String>, trigger: Entity?): String? {
        return this.onRequest(dungeon, params)
    }
}
```

```kotlin
package org.serverct.ersha.dungeon.internal.dungeon.placeholder

import org.serverct.ersha.dungeon.common.api.annotation.AutoRegister
import org.serverct.ersha.dungeon.common.api.component.placeholder.DungeonPlaceholder
import org.serverct.ersha.dungeon.common.api.component.script.type.ScriptType
import org.serverct.ersha.dungeon.internal.dungeon.Dungeon

@AutoRegister(registerMessage = false)
class DungeonMobPlaceholder : DungeonPlaceholder {

    override val head: String = "mob"

    override val example: String = "<mob:kill-amount/kill-contain *怪物名>"

    override val plugin: String = "DungeonPlus"

    override fun getSupportType(): Array<ScriptType> {
        return arrayOf(ScriptType.SYSTEM, ScriptType.DUNGEON, ScriptType.PLAYER, ScriptType.TRIGGER_SELF)
    }

    override fun onRequest(dungeon: Dungeon, params: Array<String>): String? {
        val name = params[1]
        val monsterAnnal = dungeon.dungeonMeta.getOrDefault("monster-annal") {
            mutableMapOf<String, Int>()
        }

        return when (params[0]) {
            "kill-amount" -> (monsterAnnal[name] ?: 0).toString()
            "kill-contain" -> monsterAnnal.containsKey(name).toString()
            else -> null
        }
    }
}
```
