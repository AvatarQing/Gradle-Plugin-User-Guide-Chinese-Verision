# Differences between a Project and a Library Project（普通项目和库项目之间的区别）

一个库项目的main输出是一个.aar包（它代表Android的归档文件）。它组合了编译代码（例如jar包或者是本地的.so文件）和资源（manifest，res，assets）。
一个库项目同样也可以独立于应用程序生成一个测试用的apk来测试。

标识Task同样适用于库项目（`assembleDebug`，`assembleRelease`），因此在命令行上与构建一个项目没有什么不同。

其余的部分，库项目与应用程序项目一样。它们都拥有build type和product flavor，也可以生成多个aar版本。
记住大部分Build Type的配置不适用于库项目。但是你可以根据库项目是否被其它项目使用或者是否用来测试来使用自定义的sourceSet改变库项目的内容。
