# Product flavors（不同定制的产品）

一个product flavor定义了从项目中构建了一个应用的自定义版本。一个单一的项目可以同时定义多个不同的flavor来改变应用的输出。

这个新的设计概念是为了解决不同的版本之间的差异非常小的情况。虽然最项目终生成了多个定制的版本，但是它们本质上都是同一个应用，那么这种做法可能是比使用库项目更好的实现方式。

Product flavor需要在`productFlavors`这个DSL容器中声明：

    android {
        ....

        productFlavors {
            flavor1 {
                ...
            }

            flavor2 {
                ...
            }
        }
    }

这里创建了两个flavor，名为`flavor1`和`flavor2`。

---

> 注意：flavor的命名不能与已存在的_Build Type_或者`androidTest`这个_sourceSet_有冲突。
