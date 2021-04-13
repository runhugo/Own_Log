# Windows
本地版本：Python 3.6.8和2.7.15
以Python 3.6.8为主，2.7以python2调用

### 1. 安装virtualenv
```
pip install virtualenv
```
安装完成后即可使用```virtualenv```的相关命令创建python虚拟环境
（但实际不使用virtualenv管理，具体创建、激活等操作参见REFERENCE第一篇）

### 2. 安装virtualenvwrapper
```
pip install virtualenvwrapper-win
```
安装完成后需要配置环境变量，在“此电脑-属性-高级系统设置-环境变量-系统变量-新建”：
```
变量名：WORKON_HOME
值：E:\Python\pyEnvs（以后虚拟环境统计默认创建到该路径下统一管理）
```
配置成功后，还需要去更改创建脚本下的默认创建目录路径，找到virtualenvwrapper的创建脚本mkvirtualenv.bat（在E:\Python\Python36\Scripts）：
```
修改set "venvwrapper.default_workon_home=%USERPROFILE%\Envs"
修改这个路径地址就可以修改virtualenv的环境地址。默认是C:\Users\***\Envs

可改成了 【set "venvwrapper.default_workon_home=%WORKON_HOME%\Envs"】,WORKON_HOME即在系统环境变量中新定义的路径
```
修改成功后，以管理员打开cmd（如果已经打开的要关闭重新打开），使用```echo %WORKON_HOME```查看是否配置成功。
如果输出的时候配置的路径，则表示成功（此时即可使用mkvirtualenv创建虚拟环境，环境都会被创建在该路径的目录下）

### 3. VS Code的配置
假设已经创建了虚拟环境，并在虚拟环境下安装了需要的Python版本，在VS Code中需要进行相关配置使用虚拟环境的版本
进入```settings```,安装```Python插件```，然后在搜索栏搜索```python.venv```进行配置：
```
Venv Folders: 相应虚拟环境的目录
Venv Path：统一管理虚拟环境的目录，也就上边的WORKON_HOME
```
设置成功后重启VS Code，即可在左下角选择虚拟环境的Python版本

### 其他问题：
1. 在VS Code中切换至虚拟环境时，会自动运行激活虚拟环境的脚本。但是在Windows下默认时禁止运行脚本的，因此需要先修改运行脚本的Policy。
使用“win+r”，搜索“powershell”并以管理员身份打开，输入以下指令：
```
Set-ExecutionPolicy RemoteSigned
```
关于Policy的有效指令：
```
-- Restricted: 不载入任何配置文件，不运行任何脚本。 "Restricted" 是默认的。
-- AllSigned: 只有被Trusted publisher签名的脚本或者配置文件才能使用，包括你自己再本地写的脚本。
-- RemoteSigned: 对于从Internet上下载的脚本或者配置文件，只有被Trusted，publisher签名的才能使用。
-- Unrestricted: 可以载入所有配置文件，可以运行所有脚本文件. 如果你运行一个从internet下载并且没有签名的脚本，在运行之前，你会被提示需要一定的权限。
-- Bypass: 所有东西都可以使用，并且没有提示和警告。
-- Undefined: 删除当前scope被赋予的ExecutionPolicy，但是Group Policy scope的Execution Policy不会被删除。
```

REFERENCE：
- [Python虚拟环境教程](https://blog.csdn.net/qq1123642601/article/details/81359316)
- [virtualenvwrapper安装、配置及使用](https://www.cnblogs.com/alice-cj/p/11642744.html)
- [VS Code Python虚拟环境配置](https://www.jianshu.com/p/fa75d3368210)
- [修改Windows脚本运行的Policy](https://blog.csdn.net/w1254335471/article/details/106028599)
