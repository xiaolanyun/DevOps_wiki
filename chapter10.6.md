### 10.6、Android自动化构建

1、jenkins中job配置

![](image/10.6.0.png)

***

2、蒲公英平台

[蒲公英插件说明](https://www.pgyer.com/doc/view/jenkins_plugin)

[蒲公英平台api](https://www.pgyer.com/doc/api)

2.1、job参数

```
ENVIRONMENT_BUILD
release
debbug
<font color="red">打包环境:Release -正式签名包;Debug -測試签名包</font>

APP_VERSION
1.1.0
<font color="red">自定义版本号</font>

IS_JENKINS
true
<font color="red">表示包构建來自Jenkins平台</font>

BRANCH
选择分支构建

H 12 * * *

clean
-PIS_JENKINS=${IS_JENKINS}
-PAPP_VERSION=${APP_VERSION}
assemble'${ENVIRONMENT_BUILD}'



Build Environment
#${BUILD_NUMBER}_${BUILD_USER_FIRST_NAME}_${APP_VERSION}_${ENVIRONMENT_BUILD}

upload to pgyer with apiV1
pgyer uKey:472425e09de5c592ebdc0476905ba97e
pgyer api_key:250afd10fbdf0e45ad35abc072e53d10
scandir:${WORKSPACE}/apk/${ENVIRONMENT_BUILD}
file wildcard:XiaoLanYunMart-v${APP_VERSION}-${ENVIRONMENT_BUILD}-${BUILD_TIME}.apk
```

![](image/10.6.1.PNG)

***

3、androidstudio参数化注入

gradle.properties

```
APP_VERSION=1.1.0
IS_JENKINS=true
BUILD_TIME=''
```

build.gradle

```
apply plugin: 'com.android.application'

static def getDate() {
    def date = new Date()
    def formattedDate = date.format('yyyy-MM-dd-HH-mm')
    return formattedDate
}

android {
    signingConfigs {
        release {
            //由于本机打包使用的是本机上的keystore
            //而jenkins打包的是服务器上的keystore
            //两个路径不一样
            if("false".equals(IS_JENKINS))
            {
                storeFile file('./XiaoLanYunMart.jks')
            }
            else
            {
                storeFile file('./XiaoLanYunMart.jks')
            }
            keyAlias 'key0'
            keyPassword 'xiaolanyun521'
            //storeFile file('./XiaoLanYunMart.jks')
            storePassword 'xiaolanyun521'
        }
    }
    compileSdkVersion 26
    defaultConfig {
        applicationId "com.example.xiaolanyun.ldmart"
        minSdkVersion 14
        targetSdkVersion 26
        versionCode 1
        //versionName "1.0"
        versionName APP_VERSION
        testInstrumentationRunner "android.support.test.runner.AndroidJUnitRunner"
    /*
    启用multiDex支持 解决方法数 超过 64k 的问题
     */
    multiDexEnabled true
    /**
     * 支持背景模糊
     */
    renderscriptTargetApi 25
    renderscriptSupportModeEnabled true
}
buildTypes {
    release {

        debuggable true
        //代码混淆
        //minifyEnabled true
        minifyEnabled false
        /*加载默认混淆配置文件*/
        proguardFiles getDefaultProguardFile('proguard-android.txt'), 'proguard-rules.pro'
        /***
         * zipalign优化
         */
        zipAlignEnabled true
        /**
         * 移除无用的resource文件
         */
        //shrinkResources true

        /***
         * 自定义字段【true：测试地址 false：线上地址】
         */
        buildConfigField "boolean", "IS_TEST", "false"
        /***
         * 自定义字段【true: Jenkins 打包 false: AS 打包】
         */
        buildConfigField "boolean", "IS_JENKINS", "${IS_JENKINS}"

        //签名引用
        signingConfig signingConfigs.release
    }
    debug {
        debuggable true
        //minifyEnabled true//混淆
        minifyEnabled false
        zipAlignEnabled true //zipAlign优化
        //shrinkResources true //移除无用的资源文件

        /*加载默认混淆配置文件*/
        proguardFiles getDefaultProguardFile('proguard-android.txt'), 'proguard-rules.pro'

        /***
         * 自定义字段【true：测试地址 false：线上地址】
         */
        buildConfigField "boolean", "IS_TEST", "true"
        /***
         * 自定义字段【true: Jenkins 打包 false: AS 打包】
         */
        buildConfigField "boolean", "IS_JENKINS", "${IS_JENKINS}"

        //签名引用
        signingConfig signingConfigs.release
    }
}
/*修改生成的apk名字*/
android.applicationVariants.all { variant ->
    variant.outputs.all { output ->
        def newName
        //def timeNow = getDate().substring(5) // 去掉年
        def timeNow

        if ("true" == IS_JENKINS) {

            timeNow = BUILD_TIME
            if (variant.buildType.name == 'debug') {
                newName = "XiaoLanYunMart-v${APP_VERSION}-debug-${timeNow}.apk"
            } else {
                newName = "XiaoLanYunMart-v${APP_VERSION}-release-${timeNow}.apk"
            }

        } else {
            timeNow = getDate();
            newName = "XiaoLanYunMart-v${APP_VERSION}-${timeNow}-" + variant.buildType.name + ".apk"

        }

        // jenkins打包时修改输出路径保存所有打包记录

        if ("true" == IS_JENKINS) {
            // 修改输出路径
            if ('debug' == variant.buildType.name) {
                variant.getPackageApplication().outputDirectory = new File(project.rootDir.absolutePath + "/apk/debug/")
            } else {
                variant.getPackageApplication().outputDirectory = new File(project.rootDir.absolutePath + "/apk/release/")
            }
        }

        outputFileName = newName

    }
}
compileOptions {
    sourceCompatibility JavaVersion.VERSION_1_8
    targetCompatibility JavaVersion.VERSION_1_8
}
lintOptions {
    abortOnError false
    checkReleaseBuilds false
}
}

buildscript {
    repositories {
        mavenCentral()
    }
    dependencies {
        classpath 'org.greenrobot:greendao-gradle-plugin:3.2.1'
    }
}

apply plugin: 'org.greenrobot.greendao'

greendao {
    schemaVersion 1
    daoPackage 'com.example.leidong.ldmart.greendao'
    targetGenDir 'src/main/java'
}

dependencies {
    implementation fileTree(include: ['*.jar'], dir: 'libs')
    //noinspection GradleCompatible
    implementation 'com.android.support:appcompat-v7:26.1.0'
    implementation 'com.android.support.constraint:constraint-layout:1.0.2'
    testImplementation 'junit:junit:4.12'
    androidTestImplementation 'com.android.support.test:runner :1.0.1'
    androidTestImplementation 'com.android.support.test.espresso:espresso-core:3.0.1'
    /*ButterKnife*/
    implementation 'com.jakewharton:butterknife:8.8.1'
    annotationProcessor 'com.jakewharton:butterknife-compiler:8.8.1'
    /*BottomBar*/
    implementation 'com.roughike:bottom-bar:2.3.1'
    /*RecyclerView*/
    implementation 'com.android.support:recyclerview-v7:26.1.0'
    /*Gson*/
    implementation 'com.google.code.gson:gson:2.8.2'
    /*GreenDao*/
    implementation 'org.greenrobot:greendao:3.0.1'
    implementation 'org.greenrobot:greendao-generator:3.0.0'
    /*Picasso*/
    implementation 'com.squareup.picasso:picasso:2.71828'
}


```



