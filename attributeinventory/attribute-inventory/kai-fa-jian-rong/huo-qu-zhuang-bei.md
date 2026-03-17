# 获取装备

## 获取玩家背包组上的所有装备数据

* 使用 `InventoryAPI.getPlayerStore(玩家)` 获取玩家储存数据对象
* 使用 `InventoryAPI.getInventoryContent(背包组名)` 获取指定背包组对象
* 使用 `IInventoryContent.getContentItems(玩家储存对象)` 获取所有装备数据

```kotlin
fun getItems(player: Player): List<ItemStack> {
    val playerStore = InventoryAPI.getPlayerStore(player)
    val content = InventoryAPI.getInventoryContent("背包组")
    if (content != null) {
        val items = content.getContentItems(playerStore)
        return items.values.toList()
    } 
    return emptyList()
}
```

## 获取玩家背包组指定装备页上的装备数据

* 使用 `InventoryAPI.getPlayerStore(玩家)` 获取玩家储存数据对象
* 使用 `InventoryAPI.getInventoryContent(背包组名)` 获取指定背包组对象
* 使用 `IInventoryContent.getInventoryPage(页数)` 获取指定装备页对象
* 使用 `IInventoryContent.getKeyItems(玩家储存对象,装备页对象)` 获取装备数据

```kotlin
fun getItems(player: Player, index: Int): List<ItemStack> {
    val playerStore = InventoryAPI.getPlayerStore(player)
    val content = InventoryAPI.getInventoryContent("背包组")
    if (content != null) {
        val page = content.getInventoryPage(index)
        if (page != null) {
            val items = content.getKeyItems(playerStore, page)
            return items.values.toList()
        }
    }
    return emptyList()
}
```
