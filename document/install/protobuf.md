## protobuf
1、详细介绍
https://github.com/google/protobuf<br>

2、下载地址
https://github.com/google/protobuf/releases

3、选择源码安装
wget wget https://github.com/google/protobuf/archive/v3.3.0.tar.gz
解压
tar xzvf  v3.3.0.tar.gz

得到
protobuf-cpp-3.3.0

进入
cd protobuf-cpp-3.3.0

执行./autogen.sh（如果不是源码安装，可以省略这一步）

指定安装目录
./configure --prefix=/data/protobuf

编译
make

 测试，这一步很耗时间
make check

make install



3、安装遇到问题：
(1)[root@localhost protobuf-3.2.0]# ./autogen.sh
+ autoreconf -f -i -Wall,no-obsolete
configure.ac:30: error: possibly undefined macro: AC_PROG_LIBTOOL
      If this token and others are legitimate, please use m4_pattern_allow.
      See the Autoconf documentation.
autoreconf: /usr/bin/autoconf failed with exit status: 1

安装yum install libtool

(2)
make[2]: *** [google/protobuf/any.pb.lo] Error 1
make[2]: Leaving directory `/data/sofeware/protobuf-3.2.0/src'
make[1]: *** [all-recursive] Error 1
make[1]: Leaving directory `/data/sofeware/protobuf-3.2.0'
make: *** [all] Error 2

解决：https://github.com/google/protobuf/pull/2599/commits/141a1dac6ca572056c6a8b989e41f6ee213f8445

cd /data/sofeware/protobuf-3.2.0/src/google/protobuf

(3)
Make C++ implementation C++11 only
https://edwards.sdsu.edu/research/c11-on-centos-6/

步骤：
gcc --version

wget http://people.centos.org/tru/devtools-2/devtools-2.repo -O /etc/yum.repos.d/devtools-2.repo

yum upgrade

yum install devtoolset-2-gcc devtoolset-2-binutils devtoolset-2-gcc-c++

scl enable devtoolset-2 bash



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
 




