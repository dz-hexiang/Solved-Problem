#设置账户名字
$ git config --global user.name "dz-hexiang"

#设置邮箱
$ git config --global user.email 472482006@qq.com

#生成密钥
$ ssh-keygen -C '472482006@qq.com' -t rsa


#回到 GitHub 个人首页，点击 Account Settings -> SSH Public Keys -> Add another public key。
#title 可以随便取名字，Key 里面添加的内容为 id_rsa.pub 文件内所有的代码。然后点击 Apply 即可


#测试
$ ssh git@github.com
PTY allocation request failed on channel 0
Hi dz-hexiang! You've successfully authenticated, but GitHub does not provide shell access.
Connection to github.com closed.
