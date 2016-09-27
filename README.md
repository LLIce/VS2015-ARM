# VS2015-ARM
FFmpeg编译ARM文件供UWP项目使用

为了编译FFmpeg吃了不少亏,掉了不少坑.此处把正确编译过程写下


准备
git clone git://github.com/microsoft/FFmpegInterop.git
cd FFmpegInterop
git clone git://source.ffmpeg.org/ffmpeg.git

参考https://trac.ffmpeg.org/wiki/CompilationGuide/WinRT
下载
​MSYS2
​YASM
gas-preprocessor.pl


开始:

自行查看msys2安装教程.此处不赘述

msys2安装好后,修改目录下的msys2_shell.cmd 添加set MSYS2_PATH_TYPE=inherit这句话可继承上级环境

找到FFmpegInterop根目录下BuildFFmpeg.bat 添加以下两句话
set SET_FULL_PATH=1
set MSYS2_BIN="C:\msys64\usr\bin\bash.exe"

管理员运行 VS2015 x86 ARM Cross Tools Command Prompt/VS2015 x86 ARM 兼容工具命令提示符

执行以下命令

SET LIB=%VSINSTALLDIR%VC\lib\store\ARM;%VSINSTALLDIR%VC\atlmfc\lib\ARM;%UniversalCRTSdkDir%lib\%UCRTVersion%\ucrt\arm;;%UniversalCRTSdkDir%lib\%UCRTVersion%\um\arm;C:\Program Files (x86)\Windows Kits\NETFXSDK\4.6\lib\um\arm;;C:\Program Files (x86)\Windows Kits\NETFXSDK\4.6\Lib\um\arm
SET LIBPATH=%VSINSTALLDIR%VC\atlmfc\lib\ARM;%VSINSTALLDIR%VC\lib\ARM;
SET INCLUDE=%VSINSTALLDIR%VC\include;%VSINSTALLDIR%VC\atlmfc\include;%UniversalCRTSdkDir%Include\%UCRTVersion%\ucrt;%UniversalCRTSdkDir%Include\%UCRTVersion%\um;%UniversalCRTSdkDir%Include\%UCRTVersion%\shared;%UniversalCRTSdkDir%Include\%UCRTVersion%\winrt;C:\Program Files (x86)\Windows Kits\NETFXSDK\4.6\Include\um;


cd到FFmpegInterop目录 
BuildFFmpeg.bat phone8.1 win10 ARM 
等待执行完毕
