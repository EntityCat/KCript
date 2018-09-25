# KCript >>
---
 一个简单的插件框架，目前正在完善中..
 插件编写wiki施工中...    
 已经正式开源(MIT License)   
作者:[EntityCat_](http://blog.sfclub.cc/) , By [SaltedFish Troll](https://sfclub.cc/)   

## 函数列表(易语言，复制粘贴到程序即可)
.版本 2   
   
.DLL命令 Initialize, 整数型, "KCript.dll", "Initialize", , 请先使用这个初始化。   
    .参数 PluginFolder, 文本型, , 传入存放插件/SDK的文件夹名字，不需要加\,填写""则使用Plugins   
   
.DLL命令 Enable, , "KCript.dll", "Enable", , 重载插件列表   
   
.DLL命令 Trigger, , "KCript.dll", "Trigger", , 返回#header开头#end结尾的数据，自己测试   
    .参数 种类, 文本型, , 插件里的方法名   
    .参数 参数, 文本型, , 传进去的东西   
   
.DLL命令 getPluginList, 文本型, "KCript.dll", "getPluginList", , 获取插件列表(json)   
   
.DLL命令 getVersion, 文本型, "KCript.dll", "getVersion", , 获取版本，失败返回null   
    .参数 插件名字, 文本型   
   
.DLL命令 getPluginName, 文本型, "KCript.dll", "getPluginName", , 返回id对应的名字，失败返回null   
    .参数 插件ID   
   
.DLL命令 getPluginNum, 整数型, "KCript.dll", "getPluginNum", , 获取插件编号   
    .参数 插件名字, 文本型   
   
.DLL命令 freePlugin, , "KCript", "freePlugin", , 卸载某插件(释放内存)   
    .参数 插件名字, 文本型   
   
.DLL命令 getConfPath, 文本型, "KCript.dll", "getConfPath", , 获取插件配置文件夹绝对路径,带\   
    .参数 插件名字, 文本型      
	
.DLL命令 run, 文本型, "KCript.dll", "run", , 让某插件运行某方法   
    .参数 插件名字, 文本型      
    .参数 方法名称, 文本型      
	
.DLL命令 openMenu, 逻辑型, "KCript.dll", "openMenu", , 打开插件的_Menu函数(加载菜单,如果有)   
    .参数 插件名字, 文本型      
		
---
## 基本使用的例子：
Initialize () '先进行初始化才能调用下面的方法   

getPluginList () '返回一个json格式的插件列表，看起来像这样：   
`{"Num1":"Example"}`   
   Num后面是他的编号,Example就是名字   

getVersion (“Example”) ’返回这个插件的版本号   

getPluginNum (“Example”) '返回插件编号   
   
run (“Example”, “Fn”) '让Example插件触发Fn方法   
   
Trigger (“onMotd”, “Argument”) '让所有插件触发onMotd方法，并且传入Argument参数，会返回这样的数据:   
   
* #Header
* 插件名|方法:运行得到的返回值
* #End
从0.3.1-alpha开始,我们不再返回返回值,请自行在SDK里面重写您的Return方法   
   
getPluginName (1) '获取编号是1的插件的名字   
   
以下是运行结果
* “{"Num1":"Example"}”
* “0.0.1”
* 1
* “#Header
* Example|onMotd:Inputd!!
* #End”
* “Example”

---
## 插件编写:
请自己看PluginDemo.e   
目前KCript只支持插件的管理和使用，不提供回调,未来或许会`集成`   
`所以sdk还是要你自己写的，不过后期我们可能会加上模板让你们改改就能用`已经实现到callback.e   

---
## 注意事项
记得要把插件放到你指定的文件夹,如果当时填了""那就是默认的Plugins,而且回调/SDK的dll要命名成SDK.dll放进去~   
Tripper全程单线程请让插件及时返回数据..   
**demo.e请编译后测试!!!**   
   
---
## FAQ&BUG：
`当插件没有提供xxx方法的时候调用会直接出错，修复会在一个月内发布(吧)`    
已修复，不提供这个方法的插件会返回'#_404',但是性能上不是很好   
   
Q1:回调怎么玩?   
A1:全部过程都塞在`demo.e`和`callback.e`里面了，请自己翻看,在代码里面解释有时候比readme好得多   
   
Q1:我觉得这有点囊肿...   
A1:我们欢迎您发出新的Pull Request,因为作者也不是特别厉害,,   
   
Q1:未来计划?   
A1:大概是一些安全上的问题和结构优化，写了CallBack之后我又对KCript的结构有了点dark胆的想法..233
   
   
---
## 特别鸣谢名单:   
xiaoku: 指针回调思路   
   
     
	 
	 
	 
![KCript - Callback.png](https://i.loli.net/2018/08/28/5b84df3a2d88d.png)