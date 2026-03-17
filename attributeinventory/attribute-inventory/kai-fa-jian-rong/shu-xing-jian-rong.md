# 属性兼容

## AttributeHandler

```kotlin
interface AttributeHandler {

    //自定义属性处理名
    val name: String

    //是否为主控属性兼容 (如果是兼容主控属性,这里设为TRUE)
    //整个插件只会注册一个主控属性
    val mainAttributeHook: Boolean

    //注册条件 (一般用于兼容不同属性插件版本的条件判断)
    fun registerCondition(): Boolean

    //通过物品列表为玩家增加属性
    fun addSourceAttribute(player: Player, source: String, items: List<ItemStack>)

    //通过属性列表为玩家增加属性
    fun addSourceAttributeFromList(player: Player, source: String, attributes: List<String>)

    //通过 source 删除增加的属性
    fun deleteSourceAttribute(player: Player, source: String)
    
}
```

实现 **AttributeHandler** 内的所有方法后，你需要再 **onEnable** 处使用 **register()** 方法注册该属性处理，并将你的插件依赖设置新增 **AttributeInventory**

## AttributePlus V3 例子

下面是 AttributePlus V3 的兼容例子，大致如下

```kotlin
package org.serverct.nanmui.inventory.common.api.attribute.impl

import org.bukkit.Bukkit
import org.bukkit.entity.Player
import org.bukkit.inventory.ItemStack
import org.serverct.ersha.api.AttributeAPI
import org.serverct.ersha.attribute.data.AttributeSource
import org.serverct.nanmui.inventory.common.api.IInventoryPage
import org.serverct.nanmui.inventory.common.api.InventoryAPI
import org.serverct.nanmui.inventory.common.api.attribute.AttributeHandler

class AttributePlusV3 : AttributeHandler {

    override val name: String = "AttributePlus_v3"

    override val mainAttributeHook: Boolean = true

    override fun registerCondition(): Boolean {
        val plugin = Bukkit.getPluginManager().getPlugin("AttributePlus")
        if (plugin != null) {
            val description = plugin.description
            if (description.version.first() == '3') {
                return true
            }
        }
        return false
    }

    override fun addSourceAttribute(player: Player, source: String, items: List<ItemStack>) {
        val data = AttributeAPI.getAttrData(player)
        val attributeSource = AttributeSource().apply {
            items.forEach { item ->
                val attribute = AttributeSource(player, item)
                this.merge(attribute)
            }
        }

        AttributeAPI.addSourceAttribute(data, source, attributeSource)
    }

    override fun addSourceAttributeFromList(player: Player, source: String, attributes: List<String>) {
        val data = AttributeAPI.getAttrData(player)
        AttributeAPI.addSourceAttribute(data, source, attributes)
    }

    override fun deleteSourceAttribute(player: Player, source: String) {
        val data = AttributeAPI.getAttrData(player)
        AttributeAPI.takeSourceAttribute(data, source)
    }
}
```
