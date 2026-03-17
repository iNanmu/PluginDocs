# Request 命令

<details>

<summary>Send</summary>

```
/request send [player] [type] [key]

向玩家发送指定类型指定KEY的数据设置请求
发送后玩家需要再输入框输入对应内容进行数据设置
```

\[type]: filter、purchase、currency

\[key]: config.yml -> priority -> type -> key (对应的节点就是)

请在游戏内使用 Tab 按键补全 Key 参数

</details>

<details>

<summary>Set</summary>

```
/request set [player] [type] [key] [data]

为玩家将指定类型指定KEY的数据设置为 [data]
```

\[type]: filter、purchase、currency

\[key]: config.yml -> priority -> type -> key (对应的节点就是)

请在游戏内使用 Tab 按键补全 Key 参数

</details>

<details>

<summary>Reset</summary>

```
/request reset [player] [type] [key]

为玩家将指定类型指定KEY的数据进行重置
```

\[type]: filter、purchase、currency

\[key]: config.yml -> priority -> type -> key (对应的节点就是)

请在游戏内使用 Tab 按键补全 Key 参数

</details>
