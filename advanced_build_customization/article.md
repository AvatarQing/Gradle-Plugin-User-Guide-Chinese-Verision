# dex options（dex选项）

    android {
        dexOptions {
            incremental false

            preDexLibraries = false

            jumboMode = false

        }
    }

这将应用所有使用dex的task。
