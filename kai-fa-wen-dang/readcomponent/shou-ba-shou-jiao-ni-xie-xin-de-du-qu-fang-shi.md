---
description: 示例
---

# 教学

## 读取需求

读取 "物理伤害: 100 **(+100)**" 括号内的属性值

## 代码

以下代码使用 Kotlin 语言

```kotlin
@AutoRegister
class TestRead : DescriptionRead(ReadPriority.BEFORE, AttributeReadType.VALUE, true){

    override fun read(key: String, lore: String): Array<Number> {
        var array = arrayOf<Number>(0.0, 0.0)

        //判断描述内是否包含括号
        if (lore.contains("[()]".toRegex())){
            //取出括号内的值
            val value = lore.getValue("\\((.*?)\\)")
            array = arrayOf(value, value)
        }
        return array
    }

    fun String.getValue(regex: String): Double {
        val p: Pattern = Pattern.compile(regex)
        val m: Matcher = p.matcher(this)
        while (m.find()) {
            return m.group(1).replace("[^0-9.-]".toRegex(), "").toDoubleOrNull() ?: 0.0
        }
        return 0.0
    }
}
```

## 像 装备等级 这种标签该怎么写？

```kotlin
@AutoRegister
class TestRead : DescriptionRead(ReadPriority.BEFORE, AttributeReadType.BOOLEAN, true){

    //使用 @AutoIncreaseKey 注释来新增标签，如果不这样做则不会读取这个标签
    //当然你也可以使用 AttributeManager 内的 increaseKey(string: String) 方法来新增
    @AutoIncreaseKey
    val level: String = "装备等级"

    override fun condition(entity: LivingEntity, lore: String): Boolean {
        if (lore.contains(level) && entity is Player){
            //获取描述上的装备等级要求值，这边我就从简的写了
            val value = lore.split(level)[1].toIntOrNull() ?: 0
            return entity.level >= value
        }
        return true
    }
}
```

## 我要怎么才能将 **插件默认的读取方式注销** 掉？

**ReadComponent** 组件上有 **unregister** 方法,你只需要将 `AttributeValueRead().unregister()` 即可

## 后续

写完后，当然就是注册了，这里请使用 **@AutoRegister** 注释进行自动注册，最后再插件是在**plugin.yml** 依赖上加 **AttributePlus** 这样子就完成了
