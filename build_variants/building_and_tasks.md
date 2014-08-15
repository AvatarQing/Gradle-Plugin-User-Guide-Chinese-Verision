# Building and Tasks（构建和任务）

我们前面提到每一个_Build Type_会创建自己的assemble< name >task，但是_Build Variant_是_Build Type_和_Product Flavor_的组合。

当使用_Product Flavor_的时候，将会创建更多的assemble-type task。分别是：

1. assemble< Variant Name >
允许直接构建一个Variant版本，例如`assembleFlavor1Debug`。
2. assemble< Build Type Name >
允许构建指定Build Type的所有APK，例如`assembleDebug`将会构建Flavor1Debug和Flavor2Debug两个Variant版本。
3. assemble< Product Flavor Name >
允许构建指定flavor的所有APK，例如`assembleFlavor1`将会构建Flavor1Debug和Flavor1Release两个Variant版本。

另外`assemble` task会构建所有可能组合的Variant版本。
