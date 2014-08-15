# Build Types（构建类型）

默认情况下，Android Plugin会自动给项目设置同时构建应用程序的debug和release版本。
两个版本之间的不同主要围绕着能否在一个安全设备上调试，以及APK如何签名。

Debug版本采用使用通用的name/password键值对自动创建的数字证书进行签名，以防止构建过程中出现请求信息。Release版本在构建过程中没有签名，需要稍后再签名。

这些配置通过一个`BuildType`对象来配置。默认情况下，这两个实例都会被创建，分别是一个`debug`版本和一个`release`版本。

Android plugin允许像创建其他构建类型一样定制`debug`和`release`实例。这需要在`buildTypes`的DSL容器中配置：

    android {
        buildTypes {
            debug {
                applicationIdSuffix ".debug"
            }

            jnidebug.initWith(buildTypes.debug)
            jnidebug {
                packageNameSuffix ".jnidebug"
                jnidebugBuild true
            }
        }
    }

以上代码片段实现了以下功能：

* 配置默认的`debug`构建类型
    * 将debug版本的包名设置为<app package>.debug以便能够同时在一台设备上安装_debug_和_release_版本的apk。
* 创建了一个名为`jnidebug`的新构建类型，并且这个构建类型是`debug`构建类型的一个副本。
* 继续配置`jnidebug`构建类型，允许使用JNI组件，并且也添加了不一样的包名后缀。

创建一个新的构建类型就是简单的在`buildType`标签下添加一个新的元素，并且可以使用`initWith()`或者直接使用闭包来配置它。

以下是一些可能使用到的属性和默认值：

 Property name	 |Default values for debug	 |Default values for release / other
 ------------- |:-------------:| -----:
 `debuggable`	 |true	 |false
 `jniDebugBuild`	 |false	 |false
 `renderscriptDebugBuild`	 |false	 |false
 `renderscriptOptimLevel`	 |3	 |3
 `applicationIdSuffix`	 |null	 |null
 `versionNameSuffix`	 |null	 |null
 `signingConfig`	 |android.signingConfigs.debug	 |null
 `zipAlign`	 |false	 |true
 `runProguard`	 |false	 |false
 `proguardFile`	 |N/A (set only)	 |N/A (set only)
 `proguardFiles`	 |N/A (set only)	 |N/A (set only)

除了以上属性之外，_Build Type_还会受项目源码和资源影响：
对于每一个Build Type都会自动创建一个匹配的_sourceSet_。默认的路径为：

    src/<buildtypename>/

这意味着_BuildType_名称不能是_main_或者_androidTest_（因为这两个是由plugin强制实现的），并且他们互相之间都必须是唯一的。

跟其他sourceSet设置一样，Build Type的source set路径可以重新被定向：

    android {
        sourceSets.jnidebug.setRoot('foo/jnidebug')
    }

另外，每一个_Build Type_都会创建一个新的assemble<BuildTypeName>任务。

`assembleDebug`和`assembleRelease`两个Task在上面已经提到过，这里要讲这两个Task从哪里被创建。当`debug`和`release`构建类型被预创建的时候，它们的tasks就会自动创建对应的这个两个Task。

上面提到的build.gradle代码片段中也会实现`assembleJnidebug` task，并且`assemble`会像依赖于`assembleDebug`和`assembleRelease`一样依赖于`assembleJnidebug`。

提示：你可以在终端下输入gradle aJ去运行`assembleJnidebug task`。

可能会使用到的情况：

* release模式不需要，只有debug模式下才使用到的权限
* 自定义的debug实现
* 为debug模式使用不同的资源（例如当资源的值由绑定的证书决定）

_BuildType_的代码和资源通过以下方式被使用：

* manifest将被混合进app的manifest
* 代码行为只是另一个资源文件夹
* 资源将叠加到main的资源中，并替换已存在的资源。
