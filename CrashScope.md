## CrashScope

### 1.安装与运行

#### 1.1安装Android Studio

安装Android Studio并配置AVD管理器，创建相关虚拟设备（选择Nexus 5配置文件和Android 7.0），配置SDK管理器，安装25.0.1的Build Tools

(此步骤也可以用雷电模拟器代替，需使用windows系统，linux系统需要改动部分文件路径和cmd命令)

#### 1.2导入CrashScope

在idea中选择文件-导入已有项目，并在project structure中将lib设置为lib所在文件夹

#### 1.3修改相关路径

在CrashScope.java类（位于edu.semeru.android.testing包中）main方法中修改以下内容

```
		// TO BE CONFIGURED
        // This should be a path to a text file that contains a list of apk paths to be run. 
        // Each line should consist of a path to a given apk file.
        String apkFile = "apps.txt";


        // TO BE CONFIGURED
        // This path should point to the aapt tool that is included with the Android SDK.
        // The current version of CrashScope was tested with version 25.0.1
        String aaptPath = "AndroidSDK/sdk/build-tools/25.0.1";


        // TO BE CONFIGURED
        // This path should point to an empty folder where CrashScope will store some
        // both temporary data generated during execution, and the final output 
        // execution json files.
        String dataFolder = "CrashScope-Data/";
```

在runCrashScopeLocal方法中修改以下内容

```
		// TO BE CONFIGURED
        // This is the path the scripts folder in the crashscope execution engine project.
        // Should be updated to the appropriate path once you clone the project.
        String scriptsPath = "crashscope-execution-engine/scripts";

        // TO BE CONFIGURED
        // This is the path to the root of your Android SDK folder.
        // CrashScope uses various tools included with the Android SDK to ineract with devices and emualtors.
        String androidSDKPath = "/Applications/AndroidSDK/sdk";


        // These are the default emulator paths for most systems.
        // These should only be updated if you are using a non-default emulator path.
        String avdPort = "5554";
        String adbPort = "5037";
```

#### 1.4运行

启动配置好的模拟器，在apps.txt中指定需要测试的app，在文件夹下放入相关apk包，运行CrashScop的main方法

### 2.核心算法

首先根据输入的路径设定各项参数，然后对apps.txt中的app循环进行自动测试，在自动测试时，首先设定测试参数，决定GUI，text输入以及GUI探索策略，然后获取测试设备各项信息，通过dump获取组件树后开始测试，主要测试逻辑为不断循环直到所有能进行输入的组件都被测试过或者遇到程序奔溃，在遇到程序崩溃的时候记录执行信息并且重新开始测试，在对一个策略的测试结束后开始另一个策略测试，在没有策略测试后结束程序，在程序结束后将测试数据存放在数据输出目录中（也可以选择存放在数据库中）

### 3.功能模块

#### 3.1 主模块

进行自动测试循环。并将数据存放在相关目录或数据库

#### 3.2数据库模块

主要用于存放持久数据

### 4.输入输出

#### 4.1输入

apps.txt中指定测试app名

根目录下相关apk包

#### 4.2输出

测试屏幕截图

测试程序xml文件

测试结果json文件
