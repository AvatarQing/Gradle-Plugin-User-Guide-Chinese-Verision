# Single projects（独立项目）

一个项目将会自动生成测试运行。默认位置为：build/reports/androidTests

这非常类似于JUnit的报告所在位置build/reports/tests，其它的报告通常位于build/reports/< plugin >/。

这个路径也可以通过以下方式自定义：

    android {
        ...

        testOptions {
            reportDir = "$project.buildDir/foo/report"
        }
    }

报告将会合并运行在不同设备上的测试结果。
