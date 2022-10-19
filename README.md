# quick-setup-mysql-on-ubuntu
MySQL-on-ubuntu

# based-on-Parallels-Desktop
# system setup
0. install Linux
1.建立vim設定檔
~~~
vi ~/.vimrc
~~~
add
~~~
set nu
set ai
set cursorline
set bg=light
setlocal list
set listchars=tab:>~,trail:.
set ts=4
set expandtab
set smartindent
~~~
2. change hostname
~~~
sudo vim /etc/hostname
~~~
~~~
sudo reboot
~~~
3. set static ip
~~~
sudo vim /etc/netplan/00-installer-config.yaml
~~~
~~~
# This is the network config written by 'subiquity'
network:
  renderer: networkd
  ethernets:
    enp0s5:
      addresses: [ 10.211.55.10/24 ]
      dhcp4: false
      gateway4: 10.211.55.1
      nameservers:
        addresses: [ 10.211.55.1 ]
  version: 2
~~~
這邊可以使用sudo netplan apply,但是我使用terminal ssh 連線,呼叫 net apply指令會當掉.
~~~
sudo reboot
~~~
# create pub key for github
Create key
~~~
ssh-keygen -t ed25519 -C "your_email@example.com"
~~~
Start the ssh-agent in the background.
~~~
eval "$(ssh-agent -s)"
~~~
add key to ssh-agent
~~~
ssh-add ~/.ssh/id_ed25519
~~~
cat your key and copy it.
add it to github ssh key.
~~~
cat ~/.ssh/id_ed25519.pub
~~~
set git config
~~~
git config --global user.email "your email"
~~~
~~~
git config --global user.name "your name"
~~~

# Installing MySQL on Ubuntu: Update Package Repository & Install MySQL
~~~
sudo apt update
~~~
~~~
sudo apt upgrade
~~~
~~~
sudo apt install mysql-server
~~~
~~~
mysql --version
~~~
~~~
sudo service mysql status
~~~

# 進入mysql設定root密碼
~~~
sudo mysql
~~~
~~~
ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password by '1qaz@WSX';
~~~
~~~
exit;
~~~


# 設定安全性
~~~
sudo mysql_secure_installation
~~~

不要設定的話, 直接按Enter

1.（VALIDATE PASSWORD PLUGIN）。除非想要強制執行嚴格的密碼規則，不然這並不是真正需要的。
Securing the MySQL server deployment. Connecting to MySQL using a blank password. VALIDATE PASSWORD PLUGIN can be used to test passwords and improve security. It checks the strength of password and allows the users to set only those passwords which are secure enough. Would you like to setup VALIDATE PASSWORD plugin? 

Press y|Y for Yes, any other key for No:

2. Using existing password for root.

Change the password for root ? ((Press y|Y for Yes, any other key for No) : 

3. By default, a MySQL installation has an anonymous user, allowing anyone to log into MySQL without having to have a user account created for them. This is intended only for testing, and to make the installation go a bit smoother. You should remove them before moving into a production environment.

Remove anonymous users? (Press y|Y for Yes, any other key for No) :

4. Normally, root should only be allowed to connect from 'localhost'. This ensures that someone cannot guess at the root password from the network.

Disallow root login remotely? (Press y|Y for Yes, any other key for No) :

5. By default, MySQL comes with a database named 'test' that anyone can access. This is also intended only for testing, and should be removed before moving into a production environment.

Remove test database and access to it? (Press y|Y for Yes, any other key for No) : 

6. Reloading the privilege tables will ensure that all changes made so far will take effect immediately.

Reload privilege tables now? (Press y|Y for Yes, any other key for No) :

7. All done!


