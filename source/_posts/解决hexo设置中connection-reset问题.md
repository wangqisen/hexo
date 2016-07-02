title: 解决hexo设置中Github connection reset问题
date: 2016-02-25 21:30:51
categories: Others
tags: [hexo,Github]
---
今天将之前部署在windows机器上面的hexo个人博客内容迁移到Mac上面来。过程不赘述，其实只需要将hexo目录下的文件整个打包拷贝到Mac某个目录下，然后使用
```
npm install
```
命令重新配置下hexo就可以了。由于我的静态博客托管在Github page上面，因此，需要hexo deploy上传博客内容到Github。然而此时出现了Github connection reset的错误提示。

试了一下发现github的http uri的确不能访问，怀疑是被墙掉了。因此，将hexo所在根目录下的_config,yml中的资源地址由http协议改为使用git协议，之后再次部署，发现commit成功。问题解决。

修改的地方如下所示：
```
repository: git@github.com:wangqisen/wangqisen.github.io.git

```
