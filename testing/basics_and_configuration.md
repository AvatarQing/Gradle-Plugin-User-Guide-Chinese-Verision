# Basics and Configuration（基本知识和配置）

正如前面所提到的，紧邻`main` _sourceSet_的就是`androidTest` _sourceSet_，默认路径在src/androidTest/下。
在这个测试_sourceSet_中会构建一个使用Android测试框架，并且可以部署到设备上的测试apk来测试应用程序。这里面包含单元测试，集成测试，和后续UI自动化测试。
这个测试sourceSet不应该包含AndroidManifest.xml文件，因为这个文件会自动生成。

下面这些值可能会在测试应用配置中使用到：

* `testPackageName`
* `testInstrumentationRunner`
* `testHandleProfiling`
* `testfunctionalTest`

正如前面所看到的，这些配置在defaultConfig对象中配置：

    android {
        defaultConfig {
            testPackageName "com.test.foo"
            testInstrumentationRunner "android.test.InstrumentationTestRunner"
            testHandleProfiling true
            testFunctionalTest true
        }
    }

在测试应用程序的manifest文件中，instrumentation节点的targetPackage属性值会自动使用测试应用的package名称设置，即使这个名称是通过`defaultConfig`或者_Build Type_对象自定义的。这也是manifest文件需要自动生成的一个原因。

另外，这个测试_sourceSet_也可以拥有自己的依赖。
默认情况下，应用程序和他的依赖会自动添加的测试应用的classpath中，但是也可以通过以下来扩展：

    dependencies {
        androidTestCompile 'com.google.guava:guava:11.0.2'
    }

测试应用通过`assembleTest` task来构建。`assembleTest`不依赖于main中的`assemble` task，需要手动设置运行，不能自动运行。

目前只有一个_Build Type_被测试。默认情况下是`debug` _Build Type_，但是这也可以通过以下自定义配置：

    android {
        ...
        testBuildType "staging"
    }
