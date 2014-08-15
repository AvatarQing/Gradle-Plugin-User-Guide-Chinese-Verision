# Testing（测试）

测试multi-flavors项目非常类似于测试简单的项目。

`androidTest` _sourceSet_用于定义所有flavor共用的测试，但是每一个flavor也可以有它自己特有的测试。

正如前面提到的，每一个flavor都会创建自己的测试sourceSet：

* `android.sourceSets.androidTestFlavor1`
位于src/androidTestFlavor1/
* `android.sourceSets.androidTestFlavor2`
位于src/androidTestFlavor2/

同样的，它们也可以拥有自己的依赖关系：

    dependencies {
        androidTestFlavor1Compile "..."
    }

这些测试可以通过main的标志性`deviceCheck` task或者main的`androidTest` task（当flavor被使用的时候这个task相当于一个标志性task）来执行。

每一个flavor也拥有它们自己的task来这行这些测试：androidTest< VariantName >。例如：

* `androidTestFlavor1Debug`
* `androidTestFlavor2Debug`

同样的，每一个Variant版本也会创建对应的测试APK构建task和安装或卸载task：

* `assembleFlavor1Test`
* `installFlavor1Debug`
* `installFlavor1Test`
* `uninstallFlavor1Debug`
* ...

最终的HTML报告支持根据flavor合并生成。
下面是测试结果和报告文件的路径，第一个是每一个flavor版本的结果，后面的是合并起来的结果：

* build/androidTest-results/flavors/< FlavorName >
* build/androidTest-results/all/
* build/reports/androidTests/flavors< FlavorName >
* build/reports/androidTests/all/
