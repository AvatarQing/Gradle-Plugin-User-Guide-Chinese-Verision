# General Tasks（通用任务）

添加一个插件到构建文件中将会自动创建一系列构建任务(build tasks)去执行（注：gradle属于任务驱动型构建工具，它的构建过程是基于Task的）。Java plugin和Android plugin都会创建以下task：

* `assemble`
这个task将会组合项目的所有输出。

* `check`
这个task将会执行所有检查。

* `build`
这个task将会执行assemble和check两个task的所有工作

* `clean`
这个task将会清空项目的输出。

实际上`assemble`，`check`，`build`这三个task不做任何事情。它们只是一个Task标志，用来告诉android plugin添加实际需要执行的task去完成这些工作。

这就允许你去调用相同的task，而不需要考虑当前是什么类型的项目，或者当前项目添加了什么plugin。
例如，添加了_findbugs_ plugin将会创建一个新的task并且让`check` task依赖于这个新的task。当`check` task被调用的时候，这个新的task将会先被调用。

在命令行环境中，你可以执行以下命令来获取更多高级别的task：

    gradle tasks

查看所有task列表和它们之间的依赖关系可以执行以下命令：

    gradle tasks --all

---

> 注意：Gradle会自动监视一个task声明的所有输入和输出。
两次执行`build` task并且期间项目没有任何改动，gradle将会使用UP-TO-DATE通知所有task。这意味着第二次build执行的时候不会请求任何task执行。这允许task之间互相依赖，而不会导致不需要的构建请求被执行。

---
