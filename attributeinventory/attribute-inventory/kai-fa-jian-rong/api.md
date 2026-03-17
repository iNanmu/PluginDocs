# API

## InventoryAPI

```kotlin
//获取玩家储存数据对象
@JvmStatic
fun getPlayerStore(player: Player): PlayerStore {
    return playerManager.getPlayerStore(player)
}

//获取指定背包组对象
@JvmStatic
fun getInventoryContent(pageName: String): IInventoryContent? {
    return inventoryManager.getContent(pageName)
}

//为玩家打开指定背包组界面
@JvmStatic
fun openToPlayer(player: Player, pageName: String, index: Int): Boolean {
    val content = getInventoryContent(pageName)
    if (content != null) {
        val page = content.getInventoryPage(index)
        if (page != null) {
            page.openToPlayer(player, true)
            return true
        }
    }
    return false
}
```

## IInventoryPage

```kotlin
interface IInventoryPage {

    //第几页装备页
    val index: Int

    //所属背包组
    val content: IInventoryContent
    
    //装备页内装备槽
    var equipments: MutableList<Char>

    //打开到玩家
    fun openToPlayer(player: Player, closeOriginal: Boolean = false)

}
```

## IInventoryContent

```kotlin
interface IInventoryContent {

    //背包组名
    val contentName: String

    //获取玩家在该装备页上的装备数据,当 [equipment] 为 true 时,仅获取装备槽位上的物品
    fun getItems(store: PlayerStore, page: IInventoryPage, equipment: Boolean): HashMap<Char, ItemStack>

    //获取装备页上所放置的装备,返回数据为槽位类型与对应槽位物品
    fun getKeyItems(store: PlayerStore, page: IInventoryPage): HashMap<String, ItemStack>

    //获取当前背包内容组对应玩家所放置的所有装备,返回数据为槽位类型与对应槽位物品
    fun getContentItems(store: PlayerStore): HashMap<String, ItemStack>

    //获取指定的装备页
    fun getInventoryPage(index: Int): IInventoryPage?

    //获取所有装备页
    fun getInventoryPages(): List<IInventoryPage>

    //打开到玩家
    fun openToPlayer(player: Player, pageIndex: Int = -1)

}
```
