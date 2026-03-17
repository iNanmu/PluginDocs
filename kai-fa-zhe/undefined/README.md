# 事件

## 插件事件

| 事件                  | 说明                    |
| ------------------- | --------------------- |
| DungeonEvent        | 地牢处理事件                |
| DungeonTeamEvent    | 地牢队伍事件                |
| DungeonContentEvent | 地牢内容处理事件              |
| DungeonEntityEvent  | 地牢实体事件 (套娃 Bukkit 事件) |
| DungeonPlayerEvent  | 地牢玩家事件 (套娃 Bukkit 事件) |

## 事件写法

事件写法跟平时写事件差不多，但也不完全一样，直接看例子吧

## 例子

写一个玩家在地牢内退出服务器时向全服发送 **"玩家在 XXX 地牢内退出了服务器"** 消息

```kotlin
//Kotlin 代码
@EventHandler
fun player(evt: DungeonPlayerEvent) {
    if (evt.sourceEvent is PlayerQuitEvent){
        val name = evt.player.name
        val dungeonName = evt.dungeon.dungeonName
        Bukkit.broadcastMessage("玩家 $name 在 $dungeonName 地牢内退出了服务器")
    }
}
```

```java
//Java 代码
@EventHandler
public void player(DungeonPlayerEvent evt) {
    if (evt.getSourceEvent() instanceof PlayerJoinEvent) {
        String name = evt.getPlayer().getName();
        String dungeonName = evt.getDungeon().dungeonName;
        Bukkit.broadcastMessage("玩家 " + name + " 在 " + dungeonName + " 地牢内退出了服务器");
    }
}
```

**DungeonPlayerEvent** 套用了 **Bukkit** 上的 **PlayerEvent** 事件，但这个 **事件只在地牢内才会触发DungeonEntityEvent** 与 **DungeonPlayerEvent** 相同，但他是套用了 **Bukkit** 上的 **EntityEvent** 事件，可能有小部分的事件无法使用
