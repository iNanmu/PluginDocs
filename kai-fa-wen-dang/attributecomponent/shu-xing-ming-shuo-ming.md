# AttributeName

## 说明

插件属性名分为两种，一种是 **属性默认名** 另一种是 **服务器属性名**\
\
**属性默认名(**&#x64;efaul&#x74;**):** 属性类注册时内 **attributeName** 参数所设属性名\
**服务器属性名(**&#x73;erve&#x72;**)**: 属性注册后会在 **attribute.yml** 生成对应配置，在配置里面修改的属性名就是 **服务器属性名**



[AttributeComponent](https://ersha.gitbook.io/attributeplus-pro/kai-fa-wen-dang/attributecomponent).getRandomValue(LivingEntity entity, String defaultAttributeName) \
这个方法内的 **defaultAttributeName** 即使属性默认名,因为一个属性类要调获取其他属性的值,需要通过 **属性默认名** 获取而不是使用 **服务器属性名** 获取
