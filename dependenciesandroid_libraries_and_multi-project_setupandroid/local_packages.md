# Local packages（本地包）

配置一个外部库的jar包依赖，你需要在`compile`配置中添加一个依赖。

    dependencies {
        compile files('libs/foo.jar')
    }

    android {
        ...
    }

---

> 注意：这个`dependencies` DSL标签是标准Gradle API中的一部分，所以它不属于`android`标签。

---

这个`compile`配置将被用于编译main application。它里面的所有东西都被会被添加到编译的classpath中，__同时__也会被打包进最终的APK。
以下是添加依赖时可能用到的其它一些配置选项：

* `compile`
main application（主module）。
* `androidTestCompile`
test application（测试module）。
* `debugCompile`
debug Build Type（debug类型的编译）。
* `releaseCompile`
release Build Type（发布类型的编译）。

因为没有可能去构建一个没有关联任何_Build Type_（构建类型）的APK，APK默认配置了两个或两个以上的编译配置：`compile`和< buildtype >Compile.
创建一个新的_Build Type_将会自动创建一个基于它名字的新配置。

这对于debug版本需要使用一个自定义库（为了反馈实例化的崩溃信息等）但发布版本不需要，或者它们依赖于同一个库的不同版本时会非常有用。
