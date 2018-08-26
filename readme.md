# KCript >>
---
 一个简单的插件框架，目前正在完善中..   
 已经正式开源   
作者:EntityCat_ , By [SaltedFish Troll](https://sfclub.cc/)   

## 函数列表(易语言，复制粘贴到程序即可)
.版本 2   
   
.DLL命令 Initialize, 整数型, "KCript.dll", "Initialize", , 请先使用这个初始化。   
   
.DLL命令 Enable, , "KCript.dll", "Enable", , 重载插件列表   
   
.DLL命令 Tripper, 文本型, "KCript.dll", "Tripper", , 返回#header开头#end结尾的数据，自己测试   
    .参数 种类, 文本型, , 插件里的方法名   
    .参数 参数, 文本型, , 传进去的东西   
   
.DLL命令 getPluginList, 文本型, "KCript.dll", "getPluginList", , 获取插件列表(json)   
   
.DLL命令 getVersion, 文本型, "KCript.dll", "getVersion", , 获取版本，失败返回null   
    .参数 插件名字, 文本型   
   
.DLL命令 getPluginName, 文本型, "KCript.dll", "getPluginName", , 返回id对应的名字，失败返回null   
    .参数 插件ID   
   
.DLL命令 getPluginNum, 整数型, "KCript.dll", "getPluginNum", , 获取插件编号   
    .参数 插件名字, 文本型   
   
.DLL命令 freePlugin, , "KCript", "freePlugin", 公开, 卸载某插件(释放内存)   
    .参数 插件名字, 文本型   
	
---
## 基本使用的例子：
Initialize () '先进行初始化才能调用下面的方法   

getPluginList () '返回一个json格式的插件列表，看起来像这样：   
`{"Num1":"Example"}`   
   Num后面是他的编号,Example就是名字   

getVersion (“Example”) ’返回这个插件的版本号   

getPluginNum (“Example”) '返回插件编号   

Trigger (“onMotd”, “Argument”) '让所有插件触发onMotd方法，并且传入Argument参数，会返回这样的数据:   
   
* #Header
* 插件名|方法:运行得到的返回值
* #End

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
目前KCript只支持插件的管理和使用，不提供回调   
所以sdk还是要你自己写的，不过后期我们可能会加上模板让你们改改就能用   
目前在纠结是用tcp客户端服务端通信还是内存通信..算了sdk是你们的锅   

---
## 注意事项
记得要把插件放到目录下的`\Plugins\`文件夹~   
Tripper全程单线程请让插件及时返回数据..   

---
## FAQ&BUG：
‘当插件没有提供xxx方法的时候调用会直接出错，修复会在一个月内发布(吧)’    
已修复，不提供这个方法的插件会返回'#_404',但是性能上不是很好   