## GitHub仓库

#### 一、本地仓库操作

1.初始化：git init

2.添加文件：git add 文件路径

3.提交本地仓库：git commit -m "描述"

4.查看提交历史：git log

5.提交回滚：git reset commitcode

6.本地仓库和远程仓库合并：git pull --rebase origin master

7.查看分支：git branch -v

8.设置代理：git config --global http.proxy 127.0.0.1:19180

9.取消代理：git config --global --unset http.proxy



#### 二、远程仓库操作：

1.添加远程仓库：git remote add origin url地址

2.推送本地仓库：git push -u origin master

3.克隆：git clone url地址

4.查看远程仓库：git remote -v

5.配置邮箱和用户名：
    git config --global user.email "email"
    git config --global user.nem "name"



#### 三、问题

1.远程终端挂掉：（fatal: the remote end hung up unexpectedly）

缓冲区太小：

​	git config --global http.postBuffer 524288000

2.本地仓库和远程仓库不一致（error: failed to push some refs to 'https://github.com/szhig/smart_city.git'）

提交文件，合并本地仓库和远程仓库:

​	git pull --rebase origin master



#### 四、SSH设置

1.生成ssh key

```
ssh-keygen -t rsa -C "邮箱地址"
```

2.填写key

Setting ---》SSH and GPG keys ---》New SSH key

将生成的key填入（key：C:\Users\PJM\.ssh\id_rsa.pub）
