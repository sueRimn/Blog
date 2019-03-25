# Chrome调试
## source面板查看
* 在Chrome打开页面
* 右键检查或者点击快捷键`F12`打开开发者工具
* 选择`source`面板
## Console控制台
查看打印信息或者输入一些命令进行查看
## Breakpoints打断点
![](https://zh.javascript.info/article/debugging-chrome/chrome-sources-breakpoint.png)

**断点**是调试器会自动暂停 `JavaScript `执行的地方
## Debugger命令
使用`debugger`命令来暂停代码
```JavaScript
let person = name => {
return name;
debugger;//调试在此停止
...
```
## 暂停并查看
![](https://zh.javascript.info/article/debugging-chrome/chrome-sources-debugger-pause.png)
查看当前代码的状态：
* `watch`：显示各种表达式的当前值
* `call stack(调用栈)`：显示嵌套的调用栈
* `scope作用域`：显示当前变量
## 跟踪执行
## 日志记录
