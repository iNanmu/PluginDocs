# 延迟触发任务

## 用法

`AttributeAPI.runEntityTask` 这个方法的说明请你前往 `AttributeAPI` 文档页面查看

```javascript
function runAttack(attacker, entity, handle){
  AttributeAPI.runEntityTask(10000, "测试", attacker, function(){
    print("任务开始执行了!")
  })
  return false
}
```
