在 Bukkit 中，你可以使用 `plugin.yml` 中的别名很容易地做到这一点。 下面是一个例子，你当前的 `plugin.yml` 中定义了一个命令：

```
name: ExamplePluginversion: 1.0author: YourNamemain: YourPlugin.ExamplePlugincommands:  exampleCommand:    description: Example    usage: /<command>
```

为了给一个命令做别名，在你的命令子节点上添加一个别名标签。下面是一个**别名**节点的例子:

```
name: ExamplePluginmain: YourPlugin.ExamplePluginversion: 1.0author: YourNamecommands:  exampleCommand:    description: Example    usage: /<command>    aliases: [alias1, alias2]
```

如果你要输入命令 `/alias1`，这个插件就会像你输入 `/exampleCommand` 一样。

>注意！
    Minecraft 的标签补全也会列出别名，所以如果你不想淹没标签补全，不要放太多的别名。