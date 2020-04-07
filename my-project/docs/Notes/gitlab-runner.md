# gitlab-runner

#### 运行runner
~~~shell
docker run -d --name gitlab-runner --restart always gitlab/gitlab-runner:v12.8.0
~~~
#### 注册runner
~~~shell
docker exec -it gitlab-runner gitlab-ci-multi-runner register
~~~
##### 注册信息
~~~shell
# 填写gitlab　的地址
Please enter the gitlab-ci coordinator URL (e.g. https://gitlab.com/):

# 填写gitlab　的token
Please enter the gitlab-ci token for this runner:

# 填写这个runner 的描述
Please enter the gitlab-ci description for this runner:

# 填写这个runner 的标签
Please enter the gitlab-ci tags for this runner (comma separated):

# 选择执行者的方式
Please enter the executor: shell, docker+machine, kubernetes, custom, docker-ssh, parallels, ssh, virtualbox, docker-ssh+machine, docker:

# 选择了docker 作为执行者　需要填写基础镜像
Please enter the default Docker image (e.g. ruby:2.6):
~~~