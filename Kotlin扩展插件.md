## Kotlin扩展插件

可以直接使用布局中的控件id来操作view控件, 不用再findViewById。大大提高工作效率，减少模板代码量，需要在==根目录下的build.gradle==添加`kotlin-android-extensions`插件

```kotlin
buildscript {
    ext.kotlin_version = "1.3.72"
    repositories {
        google()
        jcenter()
    }
    dependencies {
        classpath "com.android.tools.build:gradle:4.1.0"
        classpath "org.jetbrains.kotlin:kotlin-gradle-plugin:$kotlin_version"
        classpath "org.jetbrains.kotlin:kotlin-android-extensions:$kotlin_version"
    }
}
```

需要在app/build.gradle应用`kotlin-android-extensions`插件

```kotlin
plugins {
    id 'com.android.application'
    id 'kotlin-android'
    id 'kotlin-android-extensions'
}
```

