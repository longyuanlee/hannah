## maven安装
1、下载地址
https://maven.apache.org/download.cgi<br>

2、相关指令
wget http://apache.fayea.com/maven/maven-3/3.5.0/binaries/apache-maven-3.5.0-bin.tar.gz
tar xzvf apache-maven-3.5.0-bin.tar.gz
mkdir /data/maven/
mv apache-maven-3.5.0/* /data/maven/

cd /etc/profile.d
touch maven.sh

vi maven.sh
export MAVEN_HOME=/data/maven
export PATH=$PATH:$MAVEN_HOME/bin
 




