# git和TortoiseGit使用同一SSH密钥

 

1. 安装git和TortoiseGit

2. 右键，选择Git GUI here，弹出下面对话框

   ![image-20200309222830090](images/image-20200309222830090.png)

3. 点击“Help”,选择“Show SSH key”

   ![image-20200309222945192](images/image-20200309222945192.png)

4. 如果没有生成公钥，点击“Generate Key”,生成公钥，如果已经生成公钥，点击复制

5. 打开git服务器，如github，点击“setting”，选择“SSH and GPG keys”,选择“New SSK key”,将刚才复制的git公钥复制到里面，添加成功

6. 将TortoiseGit配置为和git使用同一密钥，空白地方右键-->TortoiseGit-->Settings，将Network中的SSH client改为Git目录下的ssh.exe，**注意目录为Git/usr/bin/ssh.exe**

   ![image-20200309223614512](images/image-20200309223614512.png)

![image-20200309223651952](images/image-20200309223651952.png)





# 查看谷歌浏览器保存的密码

1. 打开浏览器,点击右上角

2. 点击设置
3. 点击”自动填充“
4. 点击“密码”
5. 查看密码

