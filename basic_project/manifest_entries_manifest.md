# Manifest entries （Manifest属性）

通过SDL可以配置一下manifest选项：

* minSdkVersion
* targetSdkVersion
* versionName
* applicationId (有效的包名 -- 更多详情请查阅[ApplicationId 对比 PackageName](http://tools.android.com/tech-docs/new-build-system/applicationid-vs-packagename))
* package Name for the test application
* Instrumentation test runner

例如：

    android {
        compileSdkVersion 19
        buildToolsVersion "19.0.0"

        defaultConfig {
            versionCode 12
            versionName "2.0"
            minSdkVersion 16
            targetSdkVersion 16
        }
    }

在`android`元素中的`defaultConfig`元素中定义所有配置。

之前的Android Plugin版本使用packageName来配置manifest文件中的packageName属性。从0.11.0版本开始，你需要在build.gradle文件中使用applicationId来配置manifest文件中的packageName属性。
这是为了消除应用程序的packageName（也是程序的ID）和java包名所引起的混乱。

在构建文件中定义的强大之处在于它是动态的。
例如，可以从一个文件中或者其它自定义的逻辑代码中读取版本信息：


    def computeVersionName() {
        ...
    }

    android {
        compileSdkVersion 19
        buildToolsVersion "19.0.0"

        defaultConfig {
            versionCode 12
            versionName computeVersionName()
            minSdkVersion 16
            targetSdkVersion 16
        }
    }

注意：不要使用与在给定范围内的getter方法可能引起冲突的方法名。例如，在defaultConfig{...}中调用getVersionName()将会自动调用defaultConfig.getVersionName()方法，你自定义的getVersionName()方法就被取代掉了。

如果一个属性没有使用DSL进行设置，一些默认的属性值将会被使用。以下表格是可能使用到的值：

Property Name      |Default value in DSL object|Default value
-------------      |:-------------:            | -----:
`versionCode`        |-1     |value from manifest if present
`versionName`        |null   |value from manifest if present
`minSdkVersion`	    |-1     |value from manifest if present
`targetSdkVersion`|-1 |value from manifest if present
`applicationId`	    |null   |value from manifest if present
`testApplicationId`  |null   |applicationId + “.test”
`testInstrumentationRunner`  |null|android.test.InstrumentationTestRunner
`signingConfig`      |null   |null
`proguardFile`       |N/A (set only)     |N/A (set only)
`proguardFiles`      |N/A (set only)     |N/A (set only)

如果你在构建脚本中使用自定义代码逻辑请求这些属性，那么第二列的值将非常重要。例如，你可能会写：

    if (android.defaultConfig.testInstrumentationRunner == null) {
        // assign a better default...
    }

如果这个值一直保持null，那么在构建执行期间将会实际替换成第三列的默认值。但是在DSL元素中并没有包含这个默认值，所以，你无法查询到这个值。
除非是真的需要，这是为了预防解析应用的manifest文件。
