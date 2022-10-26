#vscode链接github
1. VSCode 默认已安装Git。

输入

git --version

如果显示版本号，则安装成功。

2. 在GitHub上新建一个仓库。例如：myrepo

3. 在本地新建一个文件夹，作为VSCode代码的工作文件夹。例如：mycode

4. mycode既是VSCode的代码工作文件夹又应该是Git的本地仓库。在命令行方式下进入mycode，输入git init

git init

5. 添加用户名和邮箱。该用户名和邮箱是注册GitHub时使用的用户名和邮箱:

    git config --global user.name "myname"
     
    git config --global user.email "myname@mymail.com"

6. 生成秘钥。继续在该目录下输入：

ssh-keygen -t rsa -C "myname@mymail.com"
然后直接一直回车，不设置密码 （也可以设置）
上面的最后一步可以在指定位置生成两个文件，并给与文件位置

打开一个名为id_rsa.pub的文件。利用文本编辑器打开该文件，全文复制。

7. 打开GitHub上的myrepo仓库，进入setting，设置deploy keys，将id_rsa.pub中的内容粘贴进去即可。默认会生成该key对应的title为myname@mymail.com

8.  绑定本地文件夹和GitHub仓库：

git remote add mycode git@https://github.com/Shuyi0806/Note.git

9. 设置完成后可以做一下连接测试：

ssh -T git@github.com

10. 先进行一次拉取，再进行一次推送：(选做)

git pull --rebase mycode master
git pull mycode master

git push --force mycode master

11.  上述配置都进行完成后，就可以利用VSCode打开mycode文件夹进行相关操作。此时任何在该文件夹下出现的改变，VSCode的“源代码管理”图标上都会出现相应发生改变的文件的数字。点击“源代码管理”图片后，会列出来所有发生改变的文件名称，在文本输入框输入提交的更改概述（不要中文），进行“提交”操作。提交成功后再“同步更改”。

12.   提交完毕后检查GitHub的myrepo会发生相应的变化。如果没有变化，在VSCode中打开控制台（ctrl+`）选择“输出”，看是否有相关的错误提示，根据错误提示信息进行调整。 
13.   当出现Failed to connect to github.com port 443 after 21069 ms: Timed out时，打开本地仓所在文件夹，进入git bash here,输入
   git config --global --unset http.proxy
   git config --global --unset https.proxy
再输入git push即可
