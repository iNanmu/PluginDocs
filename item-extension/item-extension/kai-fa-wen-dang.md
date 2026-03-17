# 开发文档

## 说明

通过 **ItemExtensionAPI** 内的方法，你可以为你的插件物品兼容上 **ItemExtension** 的数据

<pre class="language-kotlin"><code class="lang-kotlin">/**
 * 新增一个装备扩展数据源
 * 注意相同的 [source] 将覆盖掉原先数据
 * 当 [item] 为 null 或 AIR 时将清除掉该源上的扩展数据
 **/
fun addItemExtensionSource(player: Player, source: String, item: ItemStack?)

/* 删除一个装备扩展数据源 */
<strong>fun removeItemExtensionSource(player: Player, source: String)
</strong>
/**
 * 将装备扩展数据更新至玩家身上
 * 使用 addItemExtensionSource / removeItemExtensionSource 方法后需手动调用
 * 尽量在你增加/删除完所有需要操作的物品扩展数据源后调用
 **/
fun updateToPlayer(player: Player)
</code></pre>
