# HybridCLR 体验项目

一个示例热更新项目。

想了解更多，请加 QQ群: 

- HybridCLR c#热更新 开发交流群：651188171
- HybridCLR 使用疑难咨询：651188171

你可以使用发布的包来体验HybridCLR热更新功能。

**示例项目使用 Unity 2020.3.33(任意后缀子版本如f1、f1c1、f1c2都可以) 版本**，2020.3.x系列都可以，但为了避免新手无谓的出错，尽量使用对应版本。

## 目录介绍

- Assets Unity项目目录
  - Main AOT主包模块
  - Hotfix 热更新模块
- HybridCLRData 包含HybridCLR的il2cpp本地安装目录

## 使用介绍

HybridCLR为c++实现，只有打包后才可使用。日常开发在编辑器下，无需打包。

如何打包出一个可热更新的包，请先参阅 [快速开始](https://focus-creative-games.github.io/hybridclr/start_up/)。

### 运行流程

本示例演示了如下几部分内容

- 将dll和资源打包成ab
- 多热更新dll，并且按依赖顺序加载它们
- 热更新脚本挂载到热更新资源中，并且正常运行
- 直接反射运行普通热更新函数App::Main

进入场景后，Main场景中的LoadDll会按顺序加载StreamingAssets目录下common AssetBundle里的HotFix.dll和HotFix2.dll，其中HotFix2.dll依赖HotFix.dll。
接着运行HotFix2.dll里的App::Main函数。

注意！多热更新dll不是必须的！大多数项目完全可以只有HotFix.dll这一个热更新模块。纯粹出于演示才故意设计了两个热更新模块。

### 体验热更新

以Win64为例，其他平台同理。

- 安装HybridCLR （安装HybridCLR的原理请看 [快速上手](https://focus-creative-games.github.io/hybridclr/start_up/)）
  - 进入HybridCLRData目录
  - 酌情修改 init_local_il2cpp_data.bat(或.sh)文件中代码
    - `set IL2CPP_BRANCH=2020.3.33` 改成与你项目Unity**年度版本匹配**的版本（2020.3.x系列选2020.3.33，2021.3.x系列选2021.3.1），注意**不是你项目的Unity版本**
    - `set IL2CPP_PATH=<你的Unity editor的il2cpp目录的路径>` 改成与上一步IL2CPP_BRANCH对应版本的Unity安装目录下的il2cpp目录
  - 运行 init_local_il2cpp_data.bat 或.sh 文件 创建本地il2cpp目录，即 LocalIl2CppData 目录。
  - **务必检查命令行的运行结果**，确保输出了 succ ，而不是其他错误。遇到错误，请先用自己对命令行的了解去解决它！！！
  - **务必检查命令行的运行结果**，确保输出了 succ ，而不是其他错误。遇到错误，请先用自己对命令行的了解去解决它！！！
  - **务必检查命令行的运行结果**，确保输出了 succ ，而不是其他错误。遇到错误，请先用自己对命令行的了解去解决它！！！
  - 重复三遍，是因为太多新手没有根据上面要求修改脚本，无脑运行而出错，却连日志都不看！！！
  - 至此完成包含HybridCLR的本地il2cpp安装
- 打包主工程
  - **请确保你已经掌握了常规的il2cpp为backend的打包过程**
  - **请确保你已经在你电脑上对于一个未使用HybrildCLR的项目成功打包出il2cpp为backend的相应包**
  - **请确保你已经在你电脑上对于一个未使用HybrildCLR的项目成功打包出il2cpp为backend的相应包**
  - **请确保你已经在你电脑上对于一个未使用HybrildCLR的项目成功打包出il2cpp为backend的相应包**
  - 重复三遍是因为太多新连il2cpp模块都没安装，也不了解打包，就想尝试热更新，结果遇到各种低级的错误来群里问。请自行找其他人或者群解决！！！
  - **先build一次App**。由于示例项目的common ab包时包含了补充元数据dll，而补充元数据必须是打包过程中生成的裁剪后的AOT dll。
  - build ab包。点击菜单`huatuo/BuildBundles/Win64`，生成Win64目标的AssetBundle，生成的AssetBundle文件会自动复制到StreamingAssets目录下
  - 运行，会看到打出 hello, HybridCLR.prefab
- 更新ab包
  - 修改HotFix项目的PrintHello代码，比如改成打印 "hello,world"。
  - 运行菜单 Huatuo/BuildBundles/Win64，重新生成ab
  - 将StreamingAssets下的ab包同步到打包主工程时Build目标的StreamingAsset目录，在{BuildDir}\build\bin\Huatuo_Data\StreamingAssets
- 再将运行，屏幕上会打印"hello,world"。

剩下的体验之旅，比如各种c#特性，自己体验吧。
