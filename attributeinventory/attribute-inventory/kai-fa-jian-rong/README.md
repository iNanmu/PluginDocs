# 开发兼容

## 介绍

你需要有 Kotlin、Java 及 Bukkit 开发基础，API插件可在售后群文件内下载

## 教程

* [兼容其他属性插件](shu-xing-jian-rong.md)
* [获取装备数据](huo-qu-zhuang-bei.md)
* [API](api.md)

## 事件

* ```kotlin
  /* 玩家在背包组界面翻页时触发 */
  InventoryPageUpdateEvent(val player: Player, val page: IInventoryPage, val changedState: Boolean)
  ```
* ```kotlin
  /**
   * 玩家关闭背包页时触发 (非翻页)
   * 玩家登录时刷新所有装备页时触发,该情况下 [changedState] 一定为 true
   */
  InventoryContentUpdateEvent(val player: Player, val content: IInventoryContent, val changedState: Boolean)
  ```
* ```kotlin
  /**
   * 玩家套装触发事件
   **/
  InventorySuitTriggerEvent(val player: Player, val suit: String, val number: Int, var attribute: List<String>) 
  ```
