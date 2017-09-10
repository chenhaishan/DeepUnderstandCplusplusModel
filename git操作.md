# git操作
-----
## 首先配置git
```git
git config --global user.name "chenhaishan"
git config --global user.email chen_hai_shan@yeah.net
```
## 然后创建一个仓库
```git
echo "# UNP" >> README.md
git init
git add README.md
git commit -m "first commit"
```

## 最后推到远端
```git
git remote add origin https://github.com/chenhaishan/UNP.git
git push -u origin master
```

## 提交更新
查看当前仓库的变化：
```git
git status
```
如果是添加了文件可以：
```git
git add git操作.md
```
如果是发生了修改：

如果想要保存修改可以使用：
```git
git add git操作.md
```

如果想和远端保持一致那么就可以：
```git
git checkout -- git操作.md
```

如果想删除某些文件：
```git
//删除当前目录下所有含有'pro'的文件
find . -type f -name '*pro*' -exec git rm {} \;
git status
find . -type f -name '*pro*' -exec rm -rf {} \;
//删除当前文件下所有以'build'开头的文件夹
git rm -r build*
git status
rm -rf build*
```

然后推到远端：
```git
git commit -m "此次更新的说明"
git push
```

## 更新同步
因为只有我一个人在维护，所以直接：
```git
git pull
```
