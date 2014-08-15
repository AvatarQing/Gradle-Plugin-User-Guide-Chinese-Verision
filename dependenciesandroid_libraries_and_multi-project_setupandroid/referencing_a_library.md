# Referencing a Library（引用一个库项目）

引用一个库项目的方法与引用其它项目的方法一样：

    dependencies {
        compile project(':libraries:lib1')
        compile project(':libraries:lib2')
    }

---

> 注意：如果你要引用多个库，那么排序将非常重要。这类似于旧构建系统里面的project.properties文件中的依赖排序。

---
