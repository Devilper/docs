## 										pipenv 使用

一个结合pip和virtualenv功能的工具

1.安装

~~~shell
pip install pipenv
~~~

2.使用

~~~shell
# 1.新建环境文件夹
mkdir pipenvtest
# 2.进入文件夹
cd pipenvtest
# 3.创建环境
pipenv --two # 使用当前系统的Python2版本创建环境
pipenv --three # 使用当前系统的Python3版本创建环境
pipenv --python 3.6 # 指定某一Python版本创建环境
# 4.激活虚拟环境
pipenv shell # 退出 exit
# 5.显示目录信息
pipenv --where
# 6.显示虚拟环境信息
pipenv --venv
# 7.显示Python解释器信息
pipenv --py
# 8.安装相关模块并加入到Pipfile
pipenv install request # 安装requests模块
pipenv install django==1.11 # 安装1.11版本的django模块
# 9.查看目前安装的库及其依赖
pipenv graph
# 10.检查安全漏洞
pipenv check
# 11.卸载全部包并从Pipfile中移除
pipenv uninstall --all
~~~

3.修改安装源

在`Pipfile`文件中`[source]`中的`url`属性，改为国内源，如:`https://pypi.doubanio.com/simple`

