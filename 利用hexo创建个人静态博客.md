##### 安装hexo及所需的环境
1.下载安装git
2.下载安装node
3.利用node附带安装好的npn命令安装hexo
```
npm install -g hexo-cli
```
4.安装部署插件 hexo-deployer-git。

```
npm install hexo-deployer-git --save
```

安装 Hexo 完成后，请执行下列命令，Hexo 将会在指定文件夹中新建所需要的文件。
```
$ hexo init <folder>
$ cd <folder>
$ npm install
```

5.你可以执行下列命令来创建一篇新文章。

```
$ hexo new [layout] <title>
```

6.更换主题

```
$ cd your-hexo-site
$ git clone https://github.com/iissnan/hexo-theme-next themes/next
```

