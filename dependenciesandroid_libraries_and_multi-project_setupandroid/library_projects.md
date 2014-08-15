# Library projects（库项目）

在上面的多项目配置中，`:libraries:lib1`和`:libraries:lib2`可能是一个Java项目，并且`:app`这个Android项目将会使用它们的jar包输出。

但是，如果你想要共享代码来访问Android API或者使用Android样式的资源，那么这些库就不能是通常的Java项目，而应该是Android库项目。
