# ambari-cluster-hadoop
yum update 
yum upgrade
yum install kernel-devel

vim /etc/sudoers
incluir 
aluno ALL=(ALL) ALL

yum install bzip2 unzip rsync wget net-tools


yum install mariadb-server mariadb

systemctl start mariadb.service
systemctl enable mariadb.service

mysqladmin -u root password 'dsacademy'
mysql -u root -p
select user, host, password from mysql.user;

yum install openssh-server openssh-clients
chkconfig sshd on
service sshd start
netstat -tulpn | grep 22

vi /etc/ssh/sshd_config
descomentar
Port 22
AddressFamily any
ListenAddress 0.0.0.0
PermitRootLogin yes
Incluir
AllowUsers aluno
AllowUsers root

service sshd restart

yum install java
java -version

yum install mlocate

download jdk linux 64 
descompactar 
mv /usr/local
criar link simbolico
ln -s /usr/local/jdk* /opt/jdk
ln -s /usr/lib/jvm/java*/jre /opt/jre

export variaveis de ambiente java
#Java
export JAVA_HOME=/opt/jdk
export JRE_HOME=/opt/jre
export PATH=$PATH:$JRE_HOME/bin:$JAVA_HOME/bin



https://www.if-not-true-then-false.com/2010/install-virtualbox-guest-additions-on-fedora-centos-red-hat-rhel/

download 
VBoxGuestAdditions_5.2.4.iso
acrescentar a iso como disco optico na vm

yum install epel-release

yum update
yum install dkms gcc make kernel-devel bzip2 binutils patch libgomp glibc-headers glibc-devel kernel-headers

reboot

mkdir /media/VirtualBoxGuestAdditions
mount -r /dev/cdrom /media/VirtualBoxGuestAdditions
sh /media/VirtualBoxGuestAdditions/VBoxLinuxAdditions.run


/media/jorley/DADOS/VirtualBoxVMs/DataServer02/DataServer02.vbox

Desabilitar o ipv6 da sistema 
/etc/sysctl.conf
incluir as linhas
# Desabilitar ipv6 
net.ipv6.conf.all.disable_ipv6 = 1
net.ipv6.conf.default.disable_ipv6 = 1
net.ipv6.conf.lo.disable_ipv6 = 1

Configuração ssh
ssh-keygen -t rsa
cat ~/.ssh/id_rsa.pub >> ~/.ssh/authorized_keys
chmod 600 ~/.ssh/authorized_keys

teste
ssh localhost

vi /etc/sysconfig/

https://docs.hortonworks.com/HDPDocuments/Ambari-2.6.0.0/bk_ambari-installation/content/disable_selinux_and_packagekit_and_check_the_umask_value.html

yum install -y ntp
systemctl enable ntpd

vi /etc/sysconfig/network
NETWORKING=yes
HOSTNAME=<fully.qualified.domain.name>

systemctl disable firewalld
service firewalld stop

setenforce 0
echo umask 0022 >> /etc/profile

vi etc/sysconfig/selinux
selinux = disabled

/etc/yum.repos.d

http://public-repo-1.hortonworks.com/ambari/centos7/2.x/updates/2.6.0.0/ambari.repo
http://public-repo-1.hortonworks.com/HDP/centos7/2.x/updates/2.6.3.0/hdp.repo


yum install -y ambari-agent 

Clone da VM

Reset do mac da placa de vm clonada para recuperar novo ip

vi /etc/sysconfig/network-scripts/ifcfg-enp02s
comentar # linha ipv6
acrescentar DNS1="8.8.8.8" DNS2="4.4.4.4"

hostnamectl status
alterar hostname no arquivo
vi /etc/sysconfig/network
NETWORKING=yes
HOSTNAME=<fully.qualified.domain.name>

alterar hostname com o comando
hostnamectl set-hostname "xxx"

/etc/ambari-server/conf/ambari.properties
server.startup.web.timeout=120

dataserver03
rpm -Uvh http://dev.mysql.com/get/mysql-community-release-el7-5.noarch.rpm
rpm -e --nodeps mysql-libs

OBS. O tutorial será organizado...