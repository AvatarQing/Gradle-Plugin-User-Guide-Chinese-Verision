# signing configurations（签名配置）

对一个应用程序签名需要以下：

* 一个Keystory
* 一个keystory密码
* 一个key的别名
* 一个key的密码
* 存储类型

位置，键名，两个密码，还有存储类型一起形成了签名配置。

默认情况下，`debug`被配置成使用一个debug keystory。
debug keystory使用了默认的密码和默认key及默认的key密码。
debug keystory的位置在$HOME/.android/debug.keystroe，如果对应位置不存在这个文件将会自动创建一个。

`debug` _Build Type_(构建类型) 会自动使用`debug` _SigningConfig_ (签名配置)。

可以创建其他配置或者自定义内建的默认配置。通过`signingConfigs`这个DSL容器来配置：

    android {
        signingConfigs {
            debug {
                storeFile file("debug.keystore")
            }

            myConfig {
                storeFile file("other.keystore")
                storePassword "android"
                keyAlias "androiddebugkey"
                keyPassword "android"
            }
        }

        buildTypes {
            foo {
                debuggable true
                jniDebugBuild true
                signingConfig signingConfigs.myConfig
            }
        }
    }

以上代码片段修改debug keystory的路径到项目的根目录下。在这个例子中，这将自动影响其他使用到`debug`构建类型的构建类型。

这里也创建了一个新的`Single Config`（签名配置）和一个使用这个新签名配置的新的`Build Type`（构建类型）。

---
> 注意：只有默认路径下的debug keystory不存在时会被自动创建。更改debug keystory的路径并不会自动在新路径下创建debug keystory。如果创建一个新的不同名字的_SignConfig_，但是使用默认的debug keystore路径来创建一个非默认的名字的SigningConing，那么还是会在默认路径下创建debug keystory。换句话说，会不会自动创建是根据keystory的路径来判断，而不是配置的名称。

---

> 注意：虽然经常使用项目根目录的相对路径作为keystore的路径，但是也可以使用绝对路径，尽管这并不推荐（除了自动创建出来的debug keystore）。

---

> __注意：如果你将这些文件添加到版本控制工具中，你可能不希望将密码直接写到这些文件中。下面Stack Overflow链接提供从控制台或者环境变量中获取密码的方法：
http://stackoverflow.com/questions/18328730/how-to-create-a-release-signed-apk-file-using-gradle
我们以后还会在这个指南中添加更多的详细信息。__

---
