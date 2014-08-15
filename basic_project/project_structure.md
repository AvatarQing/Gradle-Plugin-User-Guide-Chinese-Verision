# Project Structure（项目结构）

上面提到的基本的构建文件需要一个默认的文件夹结构。Gradle遵循约定优先于配置的概念，在可能的情况尽可能提供合理的默认配置参数。

基本的项目开始于两个名为“source sets”的组件，即main source code和test code。它们分别位于：

 * src/main/
 * src/androidTest/

里面每一个存在的文件夹对应相应的源组件。
对于Java plugin和Android plugin来说，它们的Java源代码和资源文件路径如下：

* java/
* resources/

但对于Android plugin来说，它还拥有以下特有的文件和文件夹结构：

* AndroidManifest.xml
* res/
* assets/
* aidl/
* rs/
* jni/

---

>注意：src/androidTest/AndroidManifest.xml是不需要的，它会自动被创建。

---
