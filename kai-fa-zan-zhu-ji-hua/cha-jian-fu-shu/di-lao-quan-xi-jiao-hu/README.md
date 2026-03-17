# 地牢全息交互

## 全息交互

即在地牢指定位置生成 **全息文字** 并设置与对应行数交互触发的地牢脚本内容，该功能需要服务器安装 **HolographicDisplays** 全息插件，可以做到很多种玩法，下方展示视频已展示了部分效果，可以自行下\
观看，目前该功能仅提供参与 **开发赞助计划** 的用户

{% file src="../../../.gitbook/assets/地牢全息交互展示视频.mp4" %}
展示视频
{% endfile %}

如果上方视频无法下载的话，请访问该 [**页面可在线观看、下载**](http://file.yiyuen.com/file/download/237634)

## 全息配置

安装插件后将自动在地牢插件文件夹内生成 **./extension**/**hologram/example.yml** 示例文件

```yaml
hologram:
  - "&e击杀 &c狂暴村民x10 &f即可通关!"
  - "&e进度 &f<mob:kill-amount *狂暴村民>&f/&63"
  - ""
  - "<if:[<mob:kill-amount *狂暴村民>>=3] *&a&l完成 &f(点击通关) *&c未完成>"

action:
  #全息行数
  4:
    #包含以下文本内容才会触发
    contain-text: "点击通关"
    #脚本
    action-script:
        #条件
      - condition: []
        #条件满足
        true:
          - "$end{type=text;text=地牢挑战成功,即将返回主城;reward=true} @dungeon"
        #条件不满足
        false: []
  #1:...
```

> **hologram** 配置项，该位置是用于设置全息文字内容，支持 **地牢占位符** 功能，当 [**Hologram** ](https://ersha.gitbook.io/dungeonplus/kai-fa-zan-zhu-ji-hua/cha-jian-fu-shu/di-lao-quan-xi-jiao-hu/hologram-jiao-ben)脚本触发类型为 **SELF** 时支持 **PlaceholderAPI** 变量\
> **action** 配置项，该位置是配置与全息列表 **对应行数点击交互所** 触发的地牢脚本效果，支持 **SELF** 类型的脚本类型

## 附属状态

| 内容       |       |
| -------- | ----- |
| **获取方式** | 插件已内置 |

