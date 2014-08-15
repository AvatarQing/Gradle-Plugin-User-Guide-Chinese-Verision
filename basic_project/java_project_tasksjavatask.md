# Java project tasks（Java项目的Task）

Java plugin主要创建了两个task，依赖于main task（一个标识性的task）：
* `assemble`
    * `jar`
    这个task创建所有输出
* `check`
    * `test`
    这个task执行所有的测试。

`jar` task自身直接或者间接依赖于其他task：`classes` task将会被调用于编译java源码。
`testClasses` task用于编译测试，但是它很少被调用，因为`test` task依赖于它（类似于`classes` task）。

通常情况下，你只需要调用到`assemble`和`check`，不需要其他task。

你可以在Gradle文档中查看[java plugin](http://gradle.org/docs/current/userguide/java_plugin.html)的全部task。
