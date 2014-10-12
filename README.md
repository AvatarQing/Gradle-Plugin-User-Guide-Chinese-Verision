Gradle Android插件用户指南翻译
---

Gradle Plugin User Guide 官方原文地址  
http://tools.android.com/tech-docs/new-build-system/user-guide

中文版在线阅读地址
http://avatarqing.github.io/Gradle-Plugin-User-Guide-Chinese-Verision/

---

本指南的翻译内容均出自于CSDN的__琴弦第七__，本人只是对其做出微小修正，对照了英文原文归纳整理成markdown格式的文本并生成gitbook，方便大家阅读学习。[翻译原文地址点此打开](http://blog.csdn.net/qinxiandiqi/article/category/2394347)。

---

__琴弦第七__

google推出了全新的Android Studio集成开发环境，其中Android项目的结构与Eclipse的Android项目结构有很大的区别，原因就在于两开发环境使用的构建工具不同。

Android Studio使用Gradle构建工具，Eclipse的ADT插件使用的是Ant构建工具。因为两个构建工具的区别，导致习惯了Eclipse开发环境的开发者刚开始比较难适应Android Studio。如果要迁移到Android Studio，建议最好了解下Gradle构建工具。Gradle构建工具是任务驱动型的构建工具，并且可以通过各种Plugin插件扩展功能以适应各种构建任务。对应Android项目的Gradle插件就是Android Gradle Plugin。本文是Google官方的Android Gradle Plugin使用指南翻译，以方便我大天朝开发者学习。如英语水平还不错的同学，建议直接查看官方原文，本人的理解和翻译难免有所疏漏。

---

License

采用[知识共享 署名-非商业性使用-相同方式共享 4.0 国际 许可协议](http://creativecommons.org/licenses/by-nc-sa/4.0/)进行许可。
