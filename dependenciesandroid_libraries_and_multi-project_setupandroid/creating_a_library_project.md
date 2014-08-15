# Creating a Library Project（创建一个库项目）

一个库项目与通常的Android项目非常类似，只是有一点小区别。

尽管构建库项目不同于构建应用程序，它们使用了不同的plugin。但是在内部这些plugin共享了大部分相同的代码，并且它们都由相同的com.android.tools.build.gradle.jar提供。

    buildscript {

        repositories {
            mavenCentral()
        }


        dependencies {
            classpath 'com.android.tools.build:gradle:0.5.6'
        }

    }

    apply plugin: 'android-library'

    android {
        compileSdkVersion 15
    }

这里创建了一个使用API 15编译_SourceSet_的库项目，并且依赖关系的配置方法与应用程序项目的配置方法一样，同样也支持自定义配置。
