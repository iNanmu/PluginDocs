# ☁️ 云端插件使用说明

## 准备内容

| 插件名                   | 获取                                                     |
| --------------------- | ------------------------------------------------------ |
| CloudPlugins (云端插件)   | 售后群获取                                                  |
| PlaceholderAPI (前置插件) | [MCBBS](https://www.mcbbs.net/thread-1216863-1-1.html) |

## 注意事项

* 如果原先 **plugins** 文件夹内安装了对应的插件 **请删除**
* 可将 **原先插件配置数据** 迁移至 **CloudPlugins** 插件文件夹内即可

## 使用步骤

* 1\. 将 **准备内容** 中的插件,安装至服务器 **./plugins** 文件夹中并启动服务器加载 **CloudPlugins** 配置文件
* 2\. 在售后群内输入 **#用户令牌** 获取你授权账户的令牌并填至 **CloudPlugins** 配置中 **user-token** 项上

```yaml
#售后群通过 #用户令牌 命令获取授权账户令牌,请勿泄露自己的令牌,否则可能被他人盗用
user-token: "sUk5ODeA2opcnd2mu0sKHyZmGj6dSHdnUBsgdG4W"
```

* 3\. 在 **CloudPlugins** 配置中 **cloud-load-plugins** 中配置所需加载的授权插件即对应版本并重启

```yaml
#将需要加载的授权插件填至下方并配置对应加载版本号
#只有授权账户中购买了对应的授权插件才会加载,否则无法加载
#可指定加载版本,也可使用 auto 自动加载最新版插件
cloud-load-plugins:
  "JobFrame": "auto"
  #"TalentAttribute": "auto"
  #"RefinePlus": "auto"
  #"StallMarket": "auto"
```

* 4\. 重启后 **CloudPlugins** 文件夹内将会生成对应授权插件的配置文件夹， **插件数据迁移** 只需要将原来在 plugins 文件夹内的配置文件夹复制至云端插件 **ColudPlugins** 配置文件夹中即可&#x20;

## 自动授权说明

从 **CloudPlugins 1.0.4** 版本起，不在需要用户手动将付费插件授权码填至对应插件配置中，你只需要将你的 **用户令牌**(上方使用步骤2) 填至 **CloudPlugins** 配置中并配置所要加载的付费插件即可

如果你需要指定使用哪个授权码的话，可在 **CloudPlugins** 配置中按以下格式添加即可

```yaml
#云端插件授权码 (付费插件)
#可指定使用授权码,没有配置或配置为 auto 时自动获取
#用户令牌所属账户上相对应付费插件的授权码
cloud-plugin-codes:
  #自动授权格式
  "JobFrame": "auto"
  #指定授权码格式
  #"StallMarket": "XXXX-XXXX-XXXX-XXXX-XXXX"
```

从该版本起请注意保护自己的用户令牌，防止泄露导致插件被他人使用，如泄露可在售后群重置令牌

## 原插件数据迁移说明

* 将原插件配置文件夹复制至 **CloudPlugins** 文件夹内即可
