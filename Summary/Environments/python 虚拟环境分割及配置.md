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

----
<br/>

# Mac OS X
系统：OS X 11.2

### 1. 安装pyenv和pyenv-virtualenv
使用```homebrew```安装：
```
brew install pyenv
brew install pyenv-virtualenv
```
安装完成后，添加路径到环境配置中(在~/.bash_profile文件中)，添加一下语句
```
# pyenv settings
export PYENV_ROOT=~/.pyenv         # 添加这句确保能切换python环境成功
export PATH="$HOME/.pyenv/bin:$PATH"
eval "$(pyenv init -)"             # 以下两句开启pyenv和virtualenv的自动补全
eval "$(pyenv virtualenv-init -)"
```

### 2. 安装python指定版本
```
pyenv install 3.6.8
(如果不知道有什么小版本，可以先输入大版本号3.6，随后会自动搜索可以安装的小版本让选择)
```
安装完成后可以通过命令行查看/切换版本
```
查看已安装版本：pyenv versions
切换:
- 全局：pyenv global 3.6.8
- 指定当前目录的python版本：pyenv local 3.6.8
```

### 3. 创建虚拟环境
```
pyenv virtualenv [python版本] [环境名字]
e.g: pyenv virtualenv 3.6.8 test_env
(若不指定 python 版本，会默认使用当前环境 python 版本)
```
查看已有的虚拟环境：
```
pyenv virtualenvs
```
激活虚拟环境：
```
pyenv activate [env name]
```
退出虚拟环境：
```
pyenv deactivate
```
删除虚拟环境：
```
pyenv uninstall env-name
rm -rf ~/.pyenv/versions/env-name  # 或者删除其真实目录
```

### 4.VS Code配置
Mac下的VS Code可以自动检测虚拟环境？
（反正我没配置...自动舅显示出来了）

### 常见问题
#### 1. 在虚拟环境下更新pip
直接更新会报以下错误：
```
Could not install packages due to an EnvironmentError: HTTPSConnectionPool(host='files.pythonhosted.org', port=443): Max retries exceeded with url: /packages/fe/ef/60d7ba03b5c442309ef42e7d69959f73aacccd0d86008362a681c4698e83/pip-21.0.1-py3-none-any.whl (Caused by NewConnectionError('<pip._vendor.urllib3.connection.VerifiedHTTPSConnection object at 0x10e2aa978>: Failed to establish a new connection: [Errno 8] nodename nor servname provided, or not known',)) 
```
要使用以下命令行：
```
python -m pip install --upgrade pip
```
#### 2. pyenv安装python报错
- 原因：可能是安装时需要饮用的包/头文件错误？
- 解决：需要指定具体的文件
- 需要工具库：openssl readline sqlite3 xz zlib
```
使用以下命令行安装：
CFLAGS="-I$(brew --prefix openssl)/include -I$(brew --prefix bzip2)/include -I$(brew --prefix readline)/include -I$(xcrun --show-sdk-path)/usr/include" \
LDFLAGS="-L$(brew --prefix openssl)/lib -L$(brew --prefix readline)/lib -L$(brew --prefix zlib)/lib -L$(brew --prefix bzip2)/lib" \ 
pyenv install --patch [python version, e.g: 3.6.8] < <(curl -sSL https://github.com/python/cpython/commit/8ea6353.patch\?full_index\=1)

(注意更换版本号)
解释：
CPPFLAGS 是 c 和 c++ 编译器的选项，这里指定了 zlib 头文件的位置，
LDFLAGS 是 gcc 等编译器会用到的一些优化参数，这里是指定了 zlib 库文件的位置，
$(brew --prefix zlib) 这一部分的意思是在终端里执行括号里的命令，显示 zlib 的安装路径，可以事先执行括号里的命令，用返回的结果替换 $(brew --prefix zlib)，效果是一样的，
每一行行尾的反斜杠可以使换行时先不执行命令，而是把这三行内容当作一条命令执行，
如果有多个依赖包都找不到，可以在引号里继续添加其它依赖包的信息

作者：夜行的鸟
链接：https://www.jianshu.com/p/c47c225e4bb5
来源：简书
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。
```


Reference:
- [使用 pyenv 管理 Python 版本 ](https://einverne.github.io/post/2017/04/pyenv.html)
- [pyenv安装python报错参考1](https://www.jianshu.com/p/c47c225e4bb5)
- [pyenv安装python报错参考2](https://github.com/pyenv/pyenv/issues/1737)