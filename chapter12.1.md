### 12.1、Maxim_Monkey使用

1、手动使用

```
adb push framework.jar /sdcard/01test

adb push monkey.jar /sdcard/01test

adb push max.config /sdcard/01test
```



普通测试;

```
adb shell CLASSPATH=/sdcard/01test/monkey.jar:/sdcard/01test/framework.jar exec app_process /system/bin tv.panda.test.monkey.Monkey -p
com.example.xiaolanyun.ldmart --uiautomatormix --running-minutes 1 -v -v
```

增加截图功能：

```
截图及dump xml
配置
Max.config 
max.takeScreenShot= true   开启截图

max.savePageSource  保存xml 
```

截图的生效条件 

throttle > 200  &&  max.takeScreenShot= true

```
adb shell CLASSPATH=/sdcard/01test/monkey.jar:/sdcard/01test/framework.jar exec app_process /system/bin tv.panda.test.monkey.Monkey
-p com.example.xiaolanyun.ldmart --uiautomatormix --running-minutes 2 -v -v
--throttle 400 --output-directory /sdcard/01test/screenshot
```



模式选择：

1、模式 DFS
   --uiautomatordfs

  增加深度遍历算法

***

2、 模式 Mix 

--uiautomatormix

直接使用底层accessibiltyserver获取界面接口 解析各控件，随机选取一个控件执行touch操作。

  同时与原monkey 其他操作按比例混合使用

  默认accessibilityserver action占比50%，其余各action分剩余的50%

  accessibilityserver action占比可配置 --pct-uiautomatormix n

***

3、模式Troy

  --uiautomatortroy

  控件选择策略按max.xpath.selector配置的高低优先级来进行深度遍历



***

