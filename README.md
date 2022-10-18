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
set smartindent
set bg=light
set tabstop=2
set shiftwidth=2
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
git config --global user.name "your name"
~~~
