
# hexo

## 安装

- node.js
- git

1. 安装 Node.js 的最佳方式是使用 nvm (Node Version Manager)

```shell
## Simple bash script to manage multiple active node.js versions
wget -qO- https://raw.githubusercontent.com/creationix/nvm/v0.31.0/install.sh | bash
```


2. 安装完成后，重启终端并执行下列命令即可安装 Node.js

```
$ nvm install 4
```

3. 安装 hexo

```
$ npm install -g hexo-cli
```


## 卸载

```shell
npm uninstall hexo-cli
```

## 使用

```shell
$ hexo init myblog
$ cd myblog
$ npm install 

$ hexo c(lean)
$ hexo g(enerate)
$ hexo s(erver)
$ hexo d(eploy)
```

## 安装主题

```shell
freematrix@shuyouMBP:~[23:28] $ cd blog
freematrix@shuyouMBP:blog[23:28] $ git clone https://github.com/iissnan/hexo-theme-next themes/next
```

## 在不同的电脑上同步写作

用 hexo 写博客的一个缺点就是源文件都是在本地的，如果换了电脑想继续更新博客则比较麻烦，不过方法总是有的：

1. 将本地的博客文件使用 github 托管
    - 在 github 下建立一个新的 repository ，名叫 blog（与hexo文件夹名一样即可）
    - 进去本地的 blog 文件夹，用命令 `git init` 创建本地仓库
    - 设置远程仓库地址 `git remote add origin git@github.com:ethan-funny/blog.git`
    - 修改 `.gitignore`文件夹，加入以下内容
    
        ```
        .DS_Store
        Thumbs.db
        db.json
        *.log
        node_modules/
        public/
        .deploy*/
        ```
    - 添加文件到暂存区，使用命令 `git add .gitignore _config.yml package.json scaffolds source themes`
    - 将这些文件提交到本地仓库，使用命令 `git commit -m "add blog files"`
    - 将本地仓库的改动推送到远程仓库，使用命令 `git push origin master`

2. 配置另外一台电脑
    - 在另外一台电脑上也安装好 `hexo` 
    - 从远程仓库 clone 博客文件，使用命令 `git clone git@github.com:ethan-funny/blog.git`
    - 进去 blog 目录，安装 hexo 插件，使用命令 `npm install`
    - 开始写作，写完后，只需要 `git add file`，再 `git commit`和 `git push`即可提交到远程仓库

3. 要注意的是，可能在另外一台电脑上也有 git 的其他用户，提交时最好配置 user.name 和 user.email
    
    ```shell
    # 项目单独配置
    $ git config user.name another_name
    $ git config user.email another_email
    ```
    
4. 再要注意的是，上面一步是对博客文件的 git 的配置，但 hexo 文件的 `.deploy_git` 目录也有自己的 `.git`配置文件，因此还要再配置一个，确保发布博客的时候是同一个用户

    ```shell
    $ cd ~/blog/.deploy_git/
    $ git config user.name another_name
    $ git config user.email another_email
    ```
    
5. 另外，由于 themes 目录里面含有其他主题，主题本身也是一个 git module，因此就涉及到`一个git仓库中嵌套一个git仓库的问题，即被嵌套的git仓库的改动，不能被大git仓库检测到`。
    - 如果该 themes 配置后就不需要改动，可以直接将它目录下的 `.git` 目录删除。
    - 也可以利用子仓库 `submodule` 的方式解决，`git submodule add https://github.com/iissnan/hexo-theme-next themes/next_origin`
    - 最终还是采取了删除 `.git`目录的做法，发现不行，向远程仓库提交 `删除整个 next 文件夹`的更改，再重新引入一个新的命名 `next2`，里面已经没有 `.git` 目录了，再提交，就可以了。


6. 将 github 托管改为由 gitlab 托管
    - 在 gitlab 下建立一个新的 repository ，名叫 blog（与hexo文件夹名一样即可）
    - 进入本地 blog 文件夹，cd ~/blog
    - git remote remove origin
    - cd .git; git remote add origin git@gitlab.com:freematrix/blog.git
    - git config user.name "Ethan"; git config user.email "freematrix@163.com"
    - git add .gitignore _config.yml package.json scaffolds source themes
    - git push --set-upstream origin master
    - 在另一台电脑上，git branch --set-upstream-to=origin/master master


## Reference

1. [nvm](https://github.com/creationix/nvm)
2. [hexo 使用文档](https://hexo.io/zh-cn/docs/)
3. [如何解决一个git仓库中嵌套一个git仓库的问题](http://www.chengyuzhang.com/article/122)
4. [Git - how to track untracked content?](http://stackoverflow.com/questions/4161022/git-how-to-track-untracked-content)
5. [使用GitHub来管理博客源文件](http://wuchong.me/blog/2014/01/17/use-github-to-manage-hexo-source/index.html)


