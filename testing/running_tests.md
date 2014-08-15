# Running tests（运行测试）

正如前面提到的，标志性task `connectedCheck`要求一个连接的设备来启动。
这个过程依赖于`androidTest` task，因此将会运行`androidTest`。这个task将会执行下面内容：

* 确认应用和测试应用都被构建（依赖于`assembleDebug`和`assembleTest`）。
* 安装这两个应用。
* 运行这些测试。
* 卸载这两个应用。

如果有多于一个连接设备，那么所有测试都会同时运行在所有连接设备上。如果其中一个测试失败，不管是哪一个设备算失败。

所有测试结果都被保存为XML文档，路径为：

    _build/androidTest-results_

（这类似于JUnit的运行结果保存在build/test-results)

同样，这也可以自定义配置：

    android {
        ...

        testOptions {
            resultsDir = "$project.buildDir/foo/results"
        }
    }

这里的`android.testOptions.resultsDir`将由`Project.file(String)`获得。
