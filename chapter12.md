### 12、Maxim_Monkey

1、An efficient Android Monkey Tester, available for emulators and real devices 基于遍历规则的高性能Android Monkey，适用于真机/模拟器的APP UI压力测试

2、支持 Android 5，6，7，8，真机及模拟器; Android 5不支持 dfs mode

3、通过Monkey程序模拟用户触摸屏幕、滑动Trackball、 按键等操作来对设备上的程序进行压力测试，检测程序多久的时间会发生异常
主要目的就是为了测试app 是否会Crash.

高速点击，每秒 10-15 action！
多平台兼容！ 同时兼容Android 5-9
轻量极简！
多策略模式：
--uiautomatormix 混合模式（70%控件解析随机点击，其余30%按原Monkey事件概率分布） 
--pct-uiautomatormix n 可自定义混合模式中控件解析事件概率
--uiautomatordfs DFS深度遍历算法（优化版）（注 Android5不支持dfs） 
--uiautomatortroy Troy模式 见 （#74楼）
非以上两种为原始Monkey策略

防跳出
控件解析时获取进程推栈Top Activity，按非白即黑立即执行切回。各事件执行时按特有逻辑屏蔽掉状态栏，防止误操作

 防休眠
休眠时自动检测并唤醒屏幕。

熔断机制
当事件按某个特有模式固定执行一段时间时则自动触发熔断开始自拉活，防止假死。如重复点击同一位置n秒

崩溃堆栈自动保存
当崩溃（crash、oom）发生时自动抓取，并存于/sdcard/crash-dump.log

崩溃回溯式截图
运行时shell增加 --imagepolling 参数 ， 开启崩溃回溯截图、关闭原截图逻辑 
当崩溃发生时 进行截图保存，实现可回溯崩溃场景，默认会在 /sdcard/crash_$timestamp/图
配置max.config

```
max.takeScreenShot = true 开启截图
max.flushImagesThreshold =xx 回溯区间大小xx张
```


截图的生效条件: throttle > 200 && max.takeScreenShot = true && --imagepolling