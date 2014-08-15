# aapt options（aapt选项）

    android {
        aaptOptions {
            noCompress 'foo', 'bar'
            ignoreAssetsPattern "!.svn:!.git:!.ds_store:!*.scc:.*:<dir>_*:!CVS:!thumbs.db:!picasa.ini:!*~"
        }
    }

这将影响所有使用aapt的task。
