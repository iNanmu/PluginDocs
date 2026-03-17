# Kether

## 说明

从 1.1.5 版本起所有地牢脚本都允许通过 Kether 方法触发，但脚本运行类型为 SYSTEM 的无法触发，同时可以通过 [**Kether(脚本)**](jiao-ben-lie-biao/kether.md) 地牢脚本触发 **Kether 脚本组 (位于** "./extension/kether" **文件夹)** 所有 Kether 的操作都可以用到地牢上了

## 单行运行

即不依靠 **Kether(脚本)** 直接在任意地牢脚本运行列表上运行 **Kether** 语句，在地牢脚本运行列表上开头不带有 **$** 符号的均视为 **Kether** 语句执行，支持 地牢占位符、变量及区域限制触发格式，下面以地牢脚本组功能为例子

```yaml
test:
  async: true
  action-script: 
    - condition: []
      true:
      #开头不带 $ 为 Kether 语句
      #当区域触发限制为 ~@ALL 时将以整个地牢内的玩家为触发者
      - actionbar *<self:player-name> 触发 Kether 语句 ~@ALL
      #开头带 $ 为地牢脚本
      - $message{type=text;text=%player_name%} @dungeon
```

## 新增语句

Kether 触发脚本方法 ([更多语句](https://kether.tabooproject.org/standard?page=private_action#dungeon))

```
dungeon *{脚本} *{运行类型} params "{参数}"
dungeon *{脚本} *{运行类型} params "{参数}" area "{区域} {区域2}"
```

Example

```
def main = {
    for i in dungeon-data players then {
        switch &i
        dungeon *message *self params "type=text;text=Example:<self:player-name>"
    }
}
```
