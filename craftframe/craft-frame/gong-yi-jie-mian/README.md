# 工艺界面

#### 基础的配置 (CONFIG.YML)

```yaml
#储存设置
sql:
  #关闭则将数据储存至本地
  enable: false
  host: localhost
  port: 3306
  user: root
  password: asd123123
  database: craft_frame

#当制作项目内某一阶段未设置 introduce 介绍时
#将显示该处设置的物品
air-introduce:
  material: BARRIER
  name: "§f无介绍"
  lore:
    - "§f该图纸暂无详细介绍"

#当未完成任意制作阶段时,界面上显示的制作物展示
air-product:
  material: BARRIER
  name: "§f暂无制作物"
  lore:
    - "§f暂未完成任意阶段的制作"
```
