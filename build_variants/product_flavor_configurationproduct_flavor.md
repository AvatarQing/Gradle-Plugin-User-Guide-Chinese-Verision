# Product Flavor Configuration（Product Flavor的配置）

每一个flavor都是通过闭包来配置的：

    android {
        ...

        defaultConfig {
            minSdkVersion 8
            versionCode 10
        }

        productFlavors {
            flavor1 {
                packageName "com.example.flavor1"
                versionCode 20
            }

            flavor2 {
                packageName "com.example.flavor2"
                minSdkVersion 14
            }
        }
    }

注意_ProductFlavor_类型的`android.productFlavors.*`对象与`android.defaultConfig`对象的类型是相同的。这意味着它们共享相同的属性。

`defaultConfig`为所有的flavor提供基本的配置，每一个flavor都可以重设这些配置的值。在上面的例子中，最终的配置结果将会是：

    * `flavor1
        * `packageName`: com.example.flavor1
        * `minSdkVersion`: 8
        * `versionCode`: 20
    * `flavor2`
        * `packageName`: com.example.flavor2
        * `minSdkVersion`: 14
        * `versionCode`: 10

通常情况下，_Build Type_的配置会覆盖其它的配置。例如，_Build Type_的`packageNameSuffix`会被追加到_Product Flavor_的`packageName`上面。

也有一些情况是一些设置可以同时在_Build Type_和_Product Flavor_中设置。在这种情况下，按照个别为主的原则决定。

例如，`signingConfig`就这种属性的一个例子。
`signingConfig`允许通过设置`android.buildTypes.release.signingConfig`来为所有的`release`包共享相同的_SigningConfig_。也可以通过设置`android.productFlavors.*.signingConfig`来为每一个release包指定它们自己的_SigningConfig_。
