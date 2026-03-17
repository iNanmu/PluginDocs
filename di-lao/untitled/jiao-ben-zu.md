---
description: 全局
---

# 脚本组

## 脚本组

即将一些脚本执行的效果写到一个组上，在任何地牢都可以通过 **命令、脚本** 进行触发，脚本组可以设置 **条件、满足执行、不满足执行、是否异步** 脚本组文件夹位于 **.../DungeonPlus/actionscript**

## 示例

```yaml
#脚本组功能
#在地牢内可使用 dp script trigger 脚本组 <触发者> 命令触发脚本组内容，触发者可有可无
#除了命令触发还有 script 脚本触发可以进行触发

#节点名不可相同
testScriptGroup:
  #是否异步默认异步处理
  async: false
  action-script:
    #必须是 @system 的判断脚本类型
    #条件
    - condition:
        - "$data-condition{key=测试数据值;type=value;value===1} @system"
      #满足条件时触发
      true:
        - "$message{type=text;text=测试数据值等于 1} @self"
      #不满足条件时触发
      false:
        - "$message{type=text;text=测试数据值不等于 1} @self"
```
