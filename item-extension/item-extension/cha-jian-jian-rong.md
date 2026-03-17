# 插件兼容

## 说明

插件支持 **AttributeInventory DragonCore** **GermPlugin**自定义槽位兼容

其中 **DragonCore** **GermPlugin** 需要通过 **config.yml** 配置进行设置哪些槽位需要读取扩展数据

提供 [API ](kai-fa-wen-dang.md)供开发者兼容

## 配置

如果你使用的是 **AttributeInventory** 那么你不需要管这部分配置

```yaml
#萌芽/龙核槽位兼容
#插件将自动开启对应插件的兼容
engine-slot-list:
  - "extension-slot"
```
