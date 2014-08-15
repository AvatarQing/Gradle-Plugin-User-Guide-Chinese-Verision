# Build Type  + Product Flavor = Build Variant（构建类型+定制产品=构建变种版本）

正如前面章节所提到的，每一个_Build Type_都会生成一个新的APK。

_Product Flavor_同样也会做这些事情：项目的输出将会拼接所有可能的_Build Type_和_Product Flavor_（如果有Flavor定义存在的话）的组合。

每一种组合（包含_Build Type_和_Product Flavor_）就是一个_Build Variant_（构建变种版本）。

例如，在上面的Flavor声明例子中与默认的`debug`和`release`两个_Build Type_将会生成4个_Build Variant_：

* Flavor1 - debug
* Flavor1 - release
* Flavor2 - debug
* Flavor2 - release

项目中如果没有定义flavor同样也会有_Build Variant_，只是使用的是默认的flavor和配置。`default`(默认)的flavor/config是没有名字的，所以生成的Build Variant列表看起来就跟_Build Type_列表一样。
