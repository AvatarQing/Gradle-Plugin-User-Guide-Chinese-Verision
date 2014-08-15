# Testing Android Libraries（测试Android库）

测试Android库项目的方法与应用项目的方法类似。

唯一的不同在于整个库（包括它的依赖）都是自动作为依赖库被添加到测试应用中。结果就是测试APK不单只包含它的代码，还包含了库项目自己和库的所有依赖。
库的manifest被组合到测试应用的manifest中（作为一些项目引用这个库的壳）。

`androidTest` task的变改只是安装（或者卸载）测试APK（因为没有其它APK被安装）。

其它的部分都是类似的。
