# Configuring the Structure

当默认的项目结构不适用的时候，你可能需要去配置它。根据Gradle文档，重新为Java项目配置_sourceSets_可以使用以下方法：

    sourceSets {
        main {
            java {
                srcDir 'src/java'
            }
            resources {
                srcDir 'src/resources'
            }
        }
    }

---

> 注意：`srcDir`将会被添加到指定的已存在的源文件夹中（这在Gradle文档中没有提到，但是实际上确实会这样执行）。

---

替换默认的源代码文件夹，你可能想要使用能够传入一个路径数组的`srcDirs`来替换单一的`srcDir`。以下是使用调用对象的另一种不同方法：

    sourceSets {
        main.java.srcDirs = ['src/java']
        main.resources.srcDirs = ['src/resources']
    }

想要获取更多信息，可以参考Gradle文档中关于[Java Pluign](http://gradle.org/docs/current/userguide/java_plugin.html)的部分。

Android Plugin使用的是类似的语法。但是由于它使用的是自己的_sourceSets_，这些配置将会被添加在`android`对象中。

以下是一个示例，它使用了旧项目结构中的main源码，并且将`androidTest` _sourceSet_组件重新映射到_tests_文件夹。

    android {
        sourceSets {
            main {
                manifest.srcFile 'AndroidManifest.xml'
                java.srcDirs = ['src']
                resources.srcDirs = ['src']
                aidl.srcDirs = ['src']
                renderscript.srcDirs = ['src']
                res.srcDirs = ['res']
                assets.srcDirs = ['assets']
            }

            androidTest.setRoot('tests')
        }
    }

---

> 注意：由于旧的项目结构将所有的源文件（java,aidl,renderscripthe和java资源文件）都放在同一个目录里面，所以我们需要将这些_sourceSet_组件重新映射到`src`目录下。

---

> 注意：`setRoot()`方法将移动整个组件（包括它的子文件夹）到一个新的文件夹。示例中将会移动`scr/androidTest/*`到`tests/*`下。
以上这些是Android特有的，如果配置在Java的_sourceSets_里面将不会有作用。

---

以上也是将旧构建系统项目迁移到新构建系统需要做的迁移工作。
