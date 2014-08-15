# Remote artifacts（远程文件）

Gradle支持从Maven或者Ivy仓库中拉取文件。

首先必须将仓库添加到列表中，然后必须在依赖中声明Maven或者Ivy声明的文件。

    repositories {
        mavenCentral()
    }


    dependencies {
        compile 'com.google.guava:guava:11.0.2'
    }

    android {
        ...
    }

---

> 注意：`mavenCentral()`是指定仓库URL的简单方法。Gradle支持远程和本地仓库。

---

> 注意：Gradle会遵循依赖关系的传递性。这意味着如果一个依赖本身依赖于其它东西，这些东西也会一并被拉取回来。

---

更多关于设置依赖关系的信息，请参考[Gradle用户指南][1]和[DSL][2]文档。

[1]: http://gradle.org/docs/current/userguide/artifact_dependencies_tutorial.html
[2]: http://gradle.org/docs/current/dsl/org.gradle.api.artifacts.dsl.DependencyHandler.html
