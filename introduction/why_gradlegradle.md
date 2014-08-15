# Why Gradle？（为什么使用gradle）
Gradle是一个优秀的构建系统和构建工具，它允许通过插件创建自定义的构建逻辑。
我们基于Gradle以下的一些特点而选择了它：

* 采用了Domain Specific Language(DSL语言)来描述和控制构建逻辑。
* 构建文件基于Groovy，并且允许通过混合声明DSL元素和使用代码来控制DSL元素以控制自定义的构建逻辑。
* 支持Maven或者Ivy的依赖管理。
* 非常灵活。允许使用最好的实现，但是不会强制实现的方式。
* 插件可以提供自己的DSL和API以供构建文件使用。
* 良好的API工具供IDE集成。
