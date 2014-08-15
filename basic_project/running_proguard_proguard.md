# Running Proguard（运行 Proguard）

从Gradle Plugin for ProGuard version 4.10之后就开始支持ProGuard。ProGuard插件是自动添加进来的。如果_Build Type_的_runProguard_属性被设置为true，对应的task将会自动创建。

    android {
        buildTypes {
            release {
                runProguard true
                proguardFile getDefaultProguardFile('proguard-android.txt')
            }
        }

        productFlavors {
            flavor1 {
            }
            flavor2 {
                proguardFile 'some-other-rules.txt'
            }
        }
    }

发布版本将会使用它的Build Type中声明的规则文件，product flavor（定制的产品版本）将会使用对应flavor中声明的规则文件。

这里有两个默认的规则文件：

* proguard-android.txt
* proguard-android-optimize.txt

这两个文件都在SDK的路径下。使用_getDefaultProguardFile()_可以获取这些文件的完整路径。它们除了是否要进行优化之外，其它都是相同的。
