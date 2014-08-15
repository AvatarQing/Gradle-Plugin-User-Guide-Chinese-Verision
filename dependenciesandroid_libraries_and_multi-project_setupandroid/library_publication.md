# Library Publication（库项目发布）

一般情况下一个库只会发布它的_release_ Variant（变种）版本。这个版本将会被所有引用它的项目使用，而不管它们本身自己构建了什么版本。这是由于Gradle的限制，我们正在努力消除这个问题，所以这只是临时的限制。

你可以控制哪一个Variant版本作为发行版：

    android {
        defaultPublishConfig "debug"
    }

注意这里的发布配置名称引用的是完整的Variant版本名称。_Relesae_，_debug_只适用于项目中没有其它特性版本的时候使用。如果你想要使用其它Variant版本取代默认的发布版本，你可以：

    android {
        defaultPublishConfig "flavor1Debug"
    }

将库项目的所有Variant版本都发布也是可能的。我们计划在一般的项目依赖项目（类似于上述所说的）情况下允许这种做法，但是由于Gradle的限制（我们也在努力修复这个问题）现在还不太可能。
默认情况下没有启用发布所有Variant版本。可以通过以下启用：

    android {
        publishNonDefault true
    }

理解发布多个Variant版本意味着发布多个arr文件而不是一个arr文件包含所有Variant版本是非常重要的。每一个arr包都包含一个单一的Variant版本。
发布一个变种版本意味着构建一个可用的arr文件作为Gradle项目的输出文件。无论是发布到一个maven仓库，还是其它项目需要创建一个这个库项目的依赖都可以使用到这个文件。

Gradle有一个默认文件的概念。当添加以下配置后就会被使用到：

    compile project(':libraries:lib2')

创建一个其它发布文件的依赖，你需要指定具体使用哪一个：

    dependencies {
        flavor1Compile project(path: ':lib1', configuration: 'flavor1Release')
        flavor2Compile project(path: ':lib1', configuration: 'flavor2Release')
    }

---

> 重要：注意已发布的配置是一个完整的Variant版本，其中包括了build type，并且需要像以上一样被引用。

---

> 重要：当启用非默认发布，maven发布插件将会发布其它Variant版本作为扩展包（按分类器分类）。这意味着不能真正的兼容发布到maven仓库。你应该另外发布一个单一的Variant版本到仓库中，或者允许发布所有配置以支持跨项目依赖。

---
