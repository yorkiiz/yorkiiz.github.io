### hexo常用指令

#### 安装git

apt-get install git

#### 安装nodejs

apt-get install nodejs

apt-get install npm

node -v

npm -v

#### 安装hexo

install -g hexo-cli

hexo -v

#### 初始化hexo

hexo init myblog

cd myblog //进入这个myblog文件夹

npm install

hexo g

hexo server

打开hexo的服务，在浏览器输入localhost:4000就可以看到你生成的博客了。

### GitHub创建个人仓库

创建一个和你用户名相同的仓库，[后面加.github.io](http://xn--yfr16an19l.github.io/)

新建分支仓库

master用于存放hexo数据，分支用于存放代码，用于分布式使用

#### github添加ssh

git config --global user.name "yourname"

 git config --global user.email "youremail"

git config user.name

 git config user.email

ssh-keygen -t rsa -C "youremail"

ssh -T git@github.com

#### 将hexo部署到github

deploy:

  type: git

  repo: https://github.com/YourgithubName/YourgithubName.github.io.git

  branch: master





hexo clean

hexo generate

hexo deploy