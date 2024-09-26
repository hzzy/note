## 配置

git config --list 查看配置 也可以查看家目录下的.gitconfig文件

git config --global color.ui auto 激活颜色选项
git config --global color.ui false 关闭颜色选项

git config --global user.name "username" 配置用户名
git config --global replace-all user.name "新的用户名" 修改用户名

git config --global user.email "email" 配置邮箱
git config --global replace-all user.email "新的邮箱" 修改邮箱


git config --global alias.co checkout 设置checkout的别名为co
