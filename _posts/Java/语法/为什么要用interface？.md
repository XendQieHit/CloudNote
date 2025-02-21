再问这个之前，我们先来想想interface的功能
```Java
package org.mcxqh.playerProfile.commands.status;  
  
import org.bukkit.command.CommandSender;  
  
public interface SubCommand {  
    void run(CommandSender sender, String[] args);  
}
```
没错，就是这样，就画个大饼和目标，就没了。就只是简单的声明说：
### 你要实现这个接口，就是要实现这些方法，要有含有这些属性。

那就会问了：
### 那我为什么不直接在我要写的类里直接写这些方法呢？直接写的话还不会因为实现接口的那行事情而报一堆错，烦死了L\[\-\_\-L\]

呃那确实是这样。

但如果你要整一个mc命令，这个命令有多个处理方法，每个方法的执行逻辑都不一样，例：
```Yaml
# ......
commands:  
  profile:  
    description: For common player, view their profile and status.  
    permission: mcxqh.profile.common  
    usage: /<command>  
  profile config:  
    description: For Server Administrator, modify this plugin's config.  
    permission: mcxqh.profile.op  
    permission-message: No permission.  
    usage: /<command> <element> <value>  
  status:  
    description: Set and view their status.  
    permission: mcxqh.profile.common  
    usage: /<command> or /<command> <list|set|custom|toggle>  
  status list:  
    description: Display their status on chat bar.  
    permission: mcxqh.profile.common  
    usage: /status list  
  status set:  
    description: Set a status which will be showed to everyone now.  
    permission: mcxqh.profile.common  
    usage: /status set <status>  
  status custom:  
    description: Set a custom name of status.  
    permission: mcxqh.profile.common  
    usage: /status custom <status> <String> [Color]  
  status toggle:  
    description: Enable or disable displaying this status.  
    permission: mcxqh.profile.common  
    usage: /status custom <status> <true|false>
```
如果我们用`switch`语句来进行每个分支的处理，也不是不可以，但是经过各种类型判断、形参数组判断、以及各类错误捕获处理，这样写出来的`status`的命令代码会有好几百行，非常不利于他人合作维护以及你自己后期维护修改。

那么`switch`语句可以被pass了，还有什么方法可以让我们更加简单明了的，一眼就能看出这个指令的逻辑结构呢？

唉，如果我们按照类的标准来进行管理，将主命令的分支语句具体逻辑分散到其他类里，是不是首先就能够处理好分支语句在主命令的判断关系呢？

ok，那么我们来弄成这样的包结构吧：
```
- commands
  - status
    - subcommands
      custom      #Class
      list        #Class
      set         #Class
      toggle      #Class
	status        #Class
```


```
- commands
  - status
    - subcommands
      custom      #Class
      list        #Class
      set         #Class
      toggle      #Class
	status        #Class
	SubCommand    #Interface
```
