# Multi-flavor variants

在一些情况下，一个应用可能需要基于多个标准来创建多个版本。例如，Google Play中的multi-apk支持4个不同的过滤器。区分创建的不同APK的每一个过滤器要求能够使用多维的Product Flavor。

假如有个游戏需要一个免费版本和一个付费的版本，并且需要在multi-apk支持中使用ABI过滤器（译注：ABI，应用二进制接口，优点是不需要改动应用的任何代码就能够将应用迁移到任何支持相同ABI的平台上）。这个游戏应用需要3个ABI和两个特定应用版本，因此就需要生成6个APK（没有因计算不同_Build Types_生成的Variant版本）。
然而，注意到在这个例子中，为三个ABI构建的付费版本源代码都是相同，因此创建6个flavor来实现不是一个好办法。
相反的，使用两个flavor维度，并且自动构建所有可能的Variant组合。

这个功能的实现就是使用Flavor Groups。每一个Group代表一个维度，并且flavor都被分配到一个指定的Group中。

    android {
        ...

        flavorGroups "abi", "version"

        productFlavors {
            freeapp {
                flavorGroup "version"
                ...
            }

            x86 {
                flavorGroup "abi"
                ...
            }

            ...
        }
    }

`andorid.flavorGroups`数组按照先后排序定义了可能使用的group。每一个_Product Flavor_都被分配到一个group中。

上面的例子中将_Product Flavor_分为两组（即两个维度），为别为abi维度[x86,arm,mips]和version维度[freeapp,paidapp]，再加上默认的_Build Type_有[debug,release]，这将会组合生成以下的Build Variant：

* x86-freeapp-debug
* x86-freeapp-release
* arm-freeapp-debug
* arm-freeapp-release
* mips-freeapp-debug
* mips-freeapp-release
* x86-paidapp-debug
* x86-paidapp-release
* arm-paidapp-debug
* arm-paidapp-release
* mips-paidapp-debug
* mips-paidapp-release

`android.flavorGroups`中定义的group排序非常重要（Variant命名和优先级等）。

每一个Variant版本的配置由几个`Product Flavor`对象决定：

* android.defaultConfig
* 一个来自abi组中的对象
* 一个来自version组中的对象

flavorGroups中的排序决定了哪一个flavor覆盖哪一个，这对于资源来说非常重要，因为一个flavor中的值会替换定义在低优先级的flavor中的值。

flavor groups使用最高的优先级定义，因此在上面例子中的优先级为：

    abi > version > defaultConfig

Multi-flavors项目同样拥有额外的sourceSet，类似于Variant的sourceSet，只是少了Build Type：

* `android.sourceSets.x86Freeapp`
位于src/x86Freeapp/
* `android.sourceSets.armPaidapp`
位于src/armPaidapp/
* 等等...

这允许在flavor-combination的层次上进行定制。它们拥有过比基础的flavor sourceSet更高的优先级，但是优先级低于Build Type的sourceSet。
