# script.yml

## 属性脚本工具配置

```yaml
#格式为 [占位符: 类] 如果不懂，请不要自己修改
scriptTools:
  "Utils": "org.serverct.ersha.script.AttrScriptUtils"
  "AttributeAPI": "org.serverct.ersha.api.AttributeAPI"
  "Bukkit": "org.bukkit.Bukkit"
  "EntityType": "org.bukkit.entity.EntityType"
  "Arrays": "java.util.Arrays"
  "Data": "org.serverct.ersha.manager.data.Data"

  #SkillAPI 扩展API
  #"SkillAPI": "com.sucy.skill.SkillAPI"
  #"SkillExtensionAPI": "org.serverct.ersha.listener.manager.skill.SkillExtensionAPI"
```

## 我想调用 其他插件 API类内的方法可以吗？

> 你只需要在 scriptTools 内新增对应内容即可，格式为 **“占位符: 包名.类名”** 例如调用 **AttributePlus** 内的 **AttributeAPI** 方法，因为 **AttributeAPI** 这个类位于插件 **org.serverct.ersha.api** 包内，所以你就需要这样写 **"AttributeAPI: org.serverct.ersha.api.AttributeAPI"**\
> \
> 这样子你就可以在属性脚本内通过占位符调用那个类内的方法啦，前提所调用的方法必须为 **static** 方法\
> \
> ~~对不具备开发能力的人来说，可能还是不知道怎么弄~~

