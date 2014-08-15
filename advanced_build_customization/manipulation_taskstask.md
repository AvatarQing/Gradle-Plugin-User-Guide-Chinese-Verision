# Manipulation tasks（操作task）

基础Java项目有一组有限的task用于互相处理生成一个输出。
`classes`是一个编译Java源代码的task。可以在build.gradle文件中通过脚本很容易使用`classes`。这是`project.tasks.classes`的缩写。

在Android项目中，相比之下这就有点复杂。因为Android项目中会有大量相同的task，并且它们的名字基于_Build Types_和_Product Flavor_生成。

为了解决这个问题，`android`对象有两个属性：

* `applicationVariants`（只适用于app plugin）
* `libraryVariants`（只适用于library plugin）
* `testVariants`（两个plugin都适用）

这三个都会分别返回一个ApplicationVariant、LibraryVariant和TestVariant对象的[DomainObjectCollection](http://www.gradle.org/docs/current/javadoc/org/gradle/api/DomainObjectCollection.html
)。

注意使用这三个collection中的其中一个都会触发生成所有对应的task。这意味着使用collection之后不需要更改配置。

DomainObjectCollection可以直接访问所有对象，或者通过过滤器进行筛选。

    android.applicationVariants.each { variant ->
        ....
    }

这三个variant类都共享下面的属性：

属性名	       	|属性类型	    |说明
-------------  	|:-------------:| -----:
name	        |String	|Variant的名字，必须是唯一的。
description		|String	|Variant的描述说明。
dirName	    	|String|Variant的子文件夹名，必须也是唯一的。可能也会有不止一个子文件夹，例如“debug/flavor1”
baseName	    |String	|Variant输出的基础名字，必须唯一。
outputFile	    |File	|Variant的输出，这是一个可读可写的属性。
processManifest	|ProcessManifest	|处理Manifest的task。
aidlCompile		|AidlCompile	|编译AIDL文件的task。
renderscriptCompile	|RenderscriptCompile    	|编译Renderscript文件的task。
mergeResources	|MergeResources	|混合资源文件的task。
mergeAssets		|MergeAssets	|混合asset的task。
processResources|ProcessAndroidResources	|处理并编译资源文件的task。
generateBuildConfig	|GenerateBuildConfig	|生成BuildConfig类的task。
javaCompile		|JavaCompile	|编译Java源代码的task。
processJavaResources|Copy	|处理Java资源的task。
assemble		|DefaultTask	|Variant的标志性assemble task。

ApplicationVariant类还有以下附加属性：

属性名			|属性类型	|说明
-------------  	|:-------------:| -----:
buildType		|BuildType	|Variant的BuildType。
productFlavors	|List<ProductFlavor>	|Variant的ProductFlavor。一般不为空但也允许空值。
mergedFlavor	|ProductFlavor	|android.defaultConfig和variant.productFlavors的合并。
signingConfig	|SigningConfig	|Variant使用的SigningConfig对象。
isSigningReady	|boolean	|如果是true则表明这个Variant已经具备了所有需要签名的信息。
testVariant		|BuildVariant	|将会测试这个Variant的TestVariant。
dex				|Dex	|将代码打包成dex的task。如果这个Variant是个库，这个值可以为空。
packageApplication	|PackageApplication	|打包最终APK的task。如果这个Variant是个库，这个值可以为空。
zipAlign		|ZipAlign	|zip压缩APK的task。如果这个Variant是个库或者APK不能被签名，这个值可以为空。
install		|DefaultTask	|负责安装的task，不能为空。
uninstall	|DefaultTask	|负责卸载的task。

LibraryVariant类还有以下附加属性：

属性名			|属性类型	|说明
-------------  	|:-------------:| -----:
buildType		|BuildType	|Variant的BuildType.
mergedFlavor	|ProductFlavor	|The defaultConfig values
testVariant		|BuildVariant	|用于测试这个Variant。
packageLibrary	|Zip	|用于打包库项目的AAR文件。如果是个库项目，这个值不能为空。

TestVariant类还有以下属性：

属性名			|属性类型	|说明
-------------  	|:-------------:| -----:
buildType	|BuildType	|Variant的Build Type。
productFlavors	|List<ProductFlavor>	|Variant的ProductFlavor。一般不为空但也允许空值。
mergedFlavor	|ProductFlavor	|android.defaultConfig和variant.productFlavors的合并。
signingConfig	|SigningConfig	|Variant使用的SigningConfig对象。
isSigningReady	|boolean	|如果是true则表明这个Variant已经具备了所有需要签名的信息。
testedVariant	|BaseVariant	|TestVariant测试的BaseVariant
dex	|Dex	|将代码打包成dex的task。如果这个Variant是个库，这个值可以为空。
packageApplication	|PackageApplication	|打包最终APK的task。如果这个Variant是个库，这个值可以为空。
zipAlign	|ZipAlign	|zip压缩APK的task。如果这个Variant是个库或者APK不能被签名，这个值可以为空。
install	|DefaultTask	|负责安装的task，不能为空。
uninstall	|DefaultTask	|负责卸载的task。
connectedAndroidTest	|DefaultTask	|在连接设备上行执行Android测试的task。
providerAndroidTest	|DefaultTask	|使用扩展API执行Android测试的task。

Android task特有类型的API：

* ProcessManifest
    * File manifestOutputFile
* AidlCompile
    * File sourceOutputDir
* RenderscriptCompile
    * File sourceOutputDir
    * File resOutputDir
* MergeResources
    * File outputDir
* MergeAssets
    * File outputDir
* ProcessAndroidResources
    * File manifestFile
    * File resDir
    * File assetsDir
    * File sourceOutputDir
    * File textSymbolOutputDir
    * File packageOutputFile
    * File proguardOutputFile
* GenerateBuildConfig
    * File sourceOutputDir
* Dex
    * File outputFolder
* PackageApplication
    * File resourceFile
    * File dexFile
    * File javaResourceDir
    * File jniDir
    * File outputFile
        * 直接在Variant对象中使用“outputFile”可以改变最终的输出文件夹。
* ZipAlign
    * File inputFile
    * File outputFile
        * 直接在Variant对象中使用“outputFile”可以改变最终的输出文件夹。

每个task类型的API由于Gradle的工作方式和Android plugin的配置方式而受到限制。
首先，Gradle意味着拥有的task只能配置输入输出的路径和一些可能使用的选项标识。因此，task只能定义一些输入或者输出。

其次，这里面大多数task的输入都不是单一的，一般都混合了_sourceSet_、_Build Type_和_Product Flavor_中的值。为了保持构建文件的简单和可读性，目标是要让开发者通过DSL语言修改这些对象来配饰构建的过程，而不是深入修改输入和task的选项。

另外需要注意，除了ZipAlign这个task类型，其它所有类型都要求设置私有数据来让它们运行。这意味着不可能自动创建这些类型的新task实例。

这些API也可能会被更改。一般来说，目前的API是围绕着给定task的输入和输出入口来添加额外的处理（如果需要的时候）。欢迎反馈意见，特别是那些没有预见过的需求。

对于Gradle的task（DefaultTask，JavaCompile，Copy，Zip），请参考Gradle文档。
