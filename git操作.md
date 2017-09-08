# git操作
-----
## 首先配置git

git config --global user.name "chenhaishan"
git config --global user.email chen_hai_shan@yeah.net

## 然后创建一个仓库
echo "# UNP" >> README.md

git init
git add README.md

git commit -m "first commit"

## 最后推到远端
git remote add origin https://github.com/chenhaishan/UNP.git
git push -u origin master

## 提交更新
查看当前仓库的变化：
git status

如果是添加了文件可以：
git add git操作.md

如果是发生了修改：

如果想要保存修改可以使用：
git add git操作.md

如果想和远端保持一致那么就可以：
git checkout -- git操作.md

然后推到远端：
git commit -m "此次更新的说明"
git push
