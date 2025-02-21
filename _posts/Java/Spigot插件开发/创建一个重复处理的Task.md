使用 Bukkit.scheduler !
```Java
Bukkit.getScheduler().scheduleSyncRepeatingTask(this, new Runnable() {  
    @Override  
    public void run() {
	    // 你要执行的任务
        StatusListener.AFKDetector();  
    }  
}, 0L, 1L); // 这里是设置延迟，代表每一个游戏刻执行一次任务,前面0延迟,后面1延迟
```