# Multi project setup（多项目设置）

Gradle项目也可以通过使用多项目配置依赖于其它Gradle项目。

多项目配置的实现通常是在一个根项目路径下将所有项目作为子文件夹包含进去。


例如，给定以下项目结构：

    MyProject/
     + app/
     + libraries/
        + lib1/
        + lib2/

我们可以定义3个项目。Grand将会按照以下名字映射它们：

    :app
    :libraries:lib1
    :libraries:lib2

每一个项目都拥有自己的build.gradle文件来声明自己如何构建。
另外，在根目录下还有一个_setting.gradle_文件用于声明所有项目。
这些文件的结构如下：

    MyProject/
     | settings.gradle
     + app/
        | build.gradle
     + libraries/
        + lib1/
           | build.gradle
        + lib2/
           | build.gradle

其中setting.gradle的内容非常简单：

    include ':app', ':libraries:lib1', ':libraries:lib2'

这里定义了哪一个文件夹才是真正的Gradle项目。

其中`:app`项目可能依赖于这些库，这是通过以下依赖配置声明的：

    dependencies {
        compile project(':libraries:lib1')
    }

更多关于多项目配置的信息请参考[这里][1]。

[1]: http://gradle.org/docs/current/userguide/multi_project_builds.html
