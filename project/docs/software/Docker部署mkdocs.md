## Docker 部署mkdocs

#### 生成目录

~~~shell
docker run -it --rm -v ~/docs:/docs squidfunk/mkdocs-material new my-project
~~~

#### 运行(后台启动)

~~~shell
docker run -it --name mkdocs --rm -v ~/docs:/docs -p 58000:8000 --workdir /docs/my-project squidfunk/mkdocs-material serve -a 0.0.0.0:8000
~~~

#### 修改配置文件

打开mkdoc.yml 文件，修改以下

~~~shell
site_name: 开发文档库
copyright: Copyright &copy; 2018 <a href="http://gisfly.xyz">gis fly</a>.
theme: 
  name: 'material'
~~~

其中主题是 `material`，保存之后就可以看到 `material` 主题了
还有另外一种主题 `readthedocs`，目录在侧边栏。

Note： *保存的时候，可能会提示没有权限，这时可以对整个文件夹进行权限修改*

```bash
sudo chmod -R 777 ~/docs/
```

在`~/docs/my-project/docs` 目录下新建文件夹，便自动生成相应的菜单。
至此，mkdocs 部署完成。



