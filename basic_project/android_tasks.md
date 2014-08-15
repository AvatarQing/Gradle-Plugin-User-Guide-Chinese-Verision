# Android tasks

Android plugin使用相同的约定以兼容其他插件，并且附加了自己的标识性task，包括：
* `assemble`
这个task用于组合项目中的所有输出。
* `check`
这个task用于执行所有检查。
* `connectedCheck`
这个task将会在一个指定的设备或者模拟器上执行检查，它们可以同时在所有连接的设备上执行。
* `deviceCheck`
通过APIs连接远程设备来执行检查，这是在CL服务器上使用的。
* `build`
这个task执行assemble和check的所有工作。
* `clean`
这个task清空项目的所有输出。

这些新的标识性task是必须的，以保证能够在没有设备连接的情况下执行定期检查。
注意`build` task不依赖于`deviceCheck`或者`connectedCheck`。

一个Android项目至少拥有两个输出：debug APK（调试版APK)和release APK（发布版APK）。每一个输出都拥有自己的标识性task以便能够单独构建它们。
* `assemble`
    * `assembleDebug`
    * `assembleRelease`

它们都依赖于其它一些tasks以完成构建一个APK需要多个步骤。其中assemble task依赖于这两个task，所以执行`assemble`将会同时构建出两个APK。

---

> 小提示：gradle在命令行终端上支持骆驼命名法的task简称，例如，执行

>       gradle aR

> 命令等同于执行

>       gradle assembleRelease。

---

check task也拥有自己的依赖：
* `check`
    * `lint`
* `connectedCheck`
    * `connectedAndroidTest`
    * `connectedUiAutomatorTest`(目前还没有应用到）
* `deviceCheck`
    * 这个test依赖于test创建时，其它实现测试扩展点的插件。

最后，只要task能够被安装（那些要求签名的task），android plugin就会为所有构建类型（`debug`，`release`，`test`）安装或者卸载。
