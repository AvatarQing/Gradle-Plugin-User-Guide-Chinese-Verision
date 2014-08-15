# Multi-projects reports（多项目报告）

在一个配置了多个应用或者多个库项目的多项目里，当同时运行所有测试的时候，生成一个报告文件记录所有的测试可能是非常有用的。

为了实现这个目的，需要使用同一个依赖文件（译注：指的是使用android gradle插件的依赖文件）中的另一个插件。可以通过以下方式添加：

    buildscript {
        repositories {
            mavenCentral()
        }

        dependencies {
            classpath 'com.android.tools.build:gradle:0.5.6'
        }
    }

apply plugin: 'android-reporting'
这必须添加到项目的根目录下，例如与settings.gradle文件同个目录的build.gradle文件中。

之后，在命令行中导航到项目根目录下，输入以下命令就可以运行所有测试并合并所有报告：

    gradle deviceCheck mergeAndroidReports --continue

---

> 注意：这里的--continue选项将允许所有测试，即使子项目中的任何一个运行失败都不会停止。如果没有这个选项，第一个失败测试将会终止全部测试的运行，这可能导致一些项目没有执行过它们的测试。

---
