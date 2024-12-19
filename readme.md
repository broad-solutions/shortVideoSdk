# 0. 前置

以下是Coolplay短剧SDK集成文档，请我们客户的开发人员参考此文档集成。同时开发人员在启动适配前，请通过商务先告知我方App的包名，我们将为该App提供集成sdk的如下clientId、clientSecret

# 1. 配置仓库地址

maven配置: 项目根目录下settings.gradle

    pluginManagement {
         repositories {
            google()
            mavenCentral()
         }
    }
    dependencyResolutionManagement {
         repositoriesMode.set(RepositoriesMode.FAIL_ON_PROJECT_REPOS)
              repositories {
                  google()
                  mavenCentral()
                  maven {
                    url = uri("https://github.com/broad-solutions/shortVideoSdk/raw/main")
                 }
                  maven {
                 url = uri("https://github.com/broad-solutions/seattleTvSdk/raw/main")
                 }
              }
    }

# 2. App's build.gradle 增加依赖包

```
dependencies {
    //短剧sdk
    implementation 'cn.coolplay:short-drama-sdk:1.0'
}
```

# 3. 初始化代码

```
在application中初始化代码

package cn.coolplay.mundonoticias

import android.app.Application
import android.content.Context
import android.util.Log
import com.tradplus.ads.open.TradPlusSdk

//初始化sdk
class App : Application() {


    override fun onCreate() {
        super.onCreate()
        //初始化sdk
        DramaSdk.initialize(this, "这里填写 clientId", "这里填写 clientSecret")", "这里是你的包名","isDebug")
    }
}
//跳转到首页
   DramaMainActivity.start(this) 
//跳转到 短剧播放页面
参数 必须是 MovieItem 这里是数据Bean
 DramaPlayActivity.start(this, "movieItem")
    DramaSdk.getRecommendList(1) {  //获取推荐列表 } 
    DramaSdk.getHotList(1) {  //获取热门列表 } 
```

# 5. 混淆配置

```
-keep class cn.coolplay.** { *; }
混淆配置已经自动处理,不需要自己填写广告相关的混淆
```

