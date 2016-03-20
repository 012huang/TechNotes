
# hexo

## 安装

- node.js
- git

1. 安装 Node.js 的最佳方式是使用 nvm (Node Version Manager)

```shell
## Simple bash script to manage multiple active node.js versions
wget -qO- https://raw.githubusercontent.com/creationix/nvm/v0.31.0/install.sh | bash
```

```
imaygou@Matrix-MacBook-Pro:~[13:17] $ wget -qO- https://raw.githubusercontent.com/creationix/nvm/v0.31.0/install.sh | bash

=> Downloading nvm from git to '/Users/imaygou/.nvm'
=> Cloning into '/Users/imaygou/.nvm'...
remote: Counting objects: 4399, done.
remote: Total 4399 (delta 0), reused 0 (delta 0), pack-reused 4399
Receiving objects: 100% (4399/4399), 1.10 MiB | 242.00 KiB/s, done.
Resolving deltas: 100% (2582/2582), done.
Checking connectivity... done.
* (HEAD detached at v0.31.0)
  master

=> Appending source string to /Users/imaygou/.zshrc
=> Close and reopen your terminal to start using nvm
```

2. 安装完成后，重启终端并执行下列命令即可安装 Node.js

```
$ nvm install 4

imaygou@Matrix-MacBook-Pro:~[13:26] $ nvm install 4
Downloading https://nodejs.org/dist/v4.3.1/node-v4.3.1-darwin-x64.tar.gz...
######################################################################## 100.0%
Now using node v4.3.1 (npm v2.14.12)
Creating default alias: default -> 4 (-> v4.3.1)

$ nvm --version
0.31.0
```

3. 安装 hexo

```
$ npm install -g hexo-cli

imaygou@Matrix-MacBook-Pro:~[13:32] $ npm install -g hexo-cli

> fsevents@1.0.8 install /Users/imaygou/.nvm/versions/node/v4.3.1/lib/node_modules/hexo-cli/node_modules/hexo-fs/node_modules/chokidar/node_modules/fsevents
> node-pre-gyp install --fallback-to-build

[fsevents] Success: "/Users/imaygou/.nvm/versions/node/v4.3.1/lib/node_modules/hexo-cli/node_modules/hexo-fs/node_modules/chokidar/node_modules/fsevents/lib/binding/Release/node-v46-darwin-x64/fse.node" is installed via remote

> dtrace-provider@0.6.0 install /Users/imaygou/.nvm/versions/node/v4.3.1/lib/node_modules/hexo-cli/node_modules/hexo-log/node_modules/bunyan/node_modules/dtrace-provider
> node scripts/install.js

---------------
Building dtrace-provider failed with exit code 1 and signal 0
re-run install with environment variable V set to see the build output
---------------

> spawn-sync@1.0.15 postinstall /Users/imaygou/.nvm/versions/node/v4.3.1/lib/node_modules/hexo-cli/node_modules/hexo-util/node_modules/cross-spawn/node_modules/spawn-sync
> node postinstall


> hexo-util@0.5.3 postinstall /Users/imaygou/.nvm/versions/node/v4.3.1/lib/node_modules/hexo-cli/node_modules/hexo-util
> npm run build:highlight


> hexo-util@0.5.3 build:highlight /Users/imaygou/.nvm/versions/node/v4.3.1/lib/node_modules/hexo-cli/node_modules/hexo-util
> node scripts/build_highlight_alias.js > highlight_alias.json

/Users/imaygou/.nvm/versions/node/v4.3.1/bin/hexo -> /Users/imaygou/.nvm/versions/node/v4.3.1/lib/node_modules/hexo-cli/bin/hexo
hexo-cli@1.0.1 /Users/imaygou/.nvm/versions/node/v4.3.1/lib/node_modules/hexo-cli
├── object-assign@4.0.1
├── abbrev@1.0.7
├── minimist@1.2.0
├── bluebird@3.3.3
├── tildify@1.1.2 (os-homedir@1.0.1)
├── chalk@1.1.1 (supports-color@2.0.0, escape-string-regexp@1.0.5, strip-ansi@3.0.1, has-ansi@2.0.0, ansi-styles@2.2.0)
├── hexo-fs@0.1.5 (escape-string-regexp@1.0.5, graceful-fs@4.1.3, chokidar@1.4.3)
├── hexo-log@0.1.2 (bunyan@1.7.1)
└── hexo-util@0.5.3 (striptags@2.1.1, html-entities@1.2.0, highlight.js@9.2.0, camel-case@1.2.2, cross-spawn@2.1.5)
```

## 卸载
npm uninstall hexo-cli

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

```
freematrix@shuyouMBP:~[23:28] $ cd blog
freematrix@shuyouMBP:blog[23:28] $ git clone https://github.com/iissnan/hexo-theme-next themes/next
```




## Reference

1. [nvm](https://github.com/creationix/nvm)
2. [hexo 使用文档](https://hexo.io/zh-cn/docs/)


