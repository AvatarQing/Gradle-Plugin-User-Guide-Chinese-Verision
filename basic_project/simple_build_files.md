# Simple build files（简单的构建文件）

一个最简单的Gradle纯Java项目的build.gradle文件包含以下内容：

    apply plugin: 'java'

这里引入了Gradle的Java插件。这个插件提供了所有构建和测试Java应用程序所需要的东西。

最简单的Android项目的build.gradle文件包含以下内容：

    buildscript {
        repositories {
            mavenCentral()
        }

        dependencies {
            classpath 'com.android.tools.build:gradle:0.11.1'
        }
    }

    apply plugin: 'android'

    android {
        compileSdkVersion 19
        buildToolsVersion "19.0.0"
    }

这里包括了Android build file的3个主要部分：

`buildscrip{...}`这里配置了驱动构建过程的代码。

在这个部分，它声明了使用Maven仓库，并且声明了一个maven文件的依赖路径。这个文件就是包含了0.11.1版本android gradle插件的库。

注意：这里的配置只影响控制构建过程的代码，不影响项目源代码。项目本身需要声明自己的仓库和依赖关系，稍后将会提到这部分。

接下来，跟前面提到的Java Plugin一样添加了`android` plugin。

最后，`andorid{...}`配置了所有android构建过程需要的参数。这里也是Android DSL的入口点。

默认情况下，只需要配置目标编译SDK版本和编译工具版本，即`compileSdkVersion`和`buildToolsVersion`属性。
这个`complieSdkVersion`属性相当于旧构建系统中project.properites文件中的`target`属性。这个新的属性可以跟旧的`target`属性一样指定一个int或者String类型的值。

---

重要：你只能添加`android` plugin。同时添加`java` plugin会导致构建错误。

注意：你同样需要在相同路径下添加一个local.properties文件，并使用sdk.dir属性来设置SDK路径。
另外，你也可以通过设置`ANDROID_HOME`环境变量，这两种方式没有什么不同，根据你自己的喜好选择其中一种设置。
