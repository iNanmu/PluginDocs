# 最基础的示例

```yaml
content-name: "简单的触发"
content-object-store: true

basic-block:
  - type: CREEPER_HEAD
    default-name: "简单的触发"
    default-skull-name: "model:grass"
basic-entity:
  - entity-collision-size: 1
    entity-type: "ARROW"
    default-name: "简单的触发"

action-steps:
  "简单的触发":
    type:
      - RIGHT_CLICK
    1:
        condition-is-met:
          - send "你右键触发了这个对象"
```
