#### 查看版本
###### cat /etc/redhat-release
#### Java 安装
- 参考：http://www.linuxidc.com/Linux/2016-09/134941.htm
+ 1.  yum search java|grep jdk
+ 2. yum install java-1.8.0-openjdk
+ 3. 安装完之后，默认的安装目录是在: /usr/lib/jvm/java。。。
+ 4. vi /etc/profile   // 设置环境变量
	+ #set java environment
	+ JAVA_HOME=/usr/lib/jvm/jdk1.8
	+ JRE_HOME=$JAVA_HOME/jre
	+ CLASS_PATH=.:$JAVA_HOME/lib/dt.jar:$JAVA_HOME/lib/tools.jar:$JRE_HOME/lib
	+ PATH=$PATH:$JAVA_HOME/bin:$JRE_HOME/bin
	+ export JAVA_HOME JRE_HOME CLASS_PATH PATH
+ 5. source /etc/profile   立即生效
+ 6. java -version  验证是否生效
#### Tomcat 安装
+ 1. 下载： wget http://mirror.bit.edu.cn/apache/tomcat/tomcat-8/v8.5.15/bin/apache-tomcat-8.5.15.tar.gz
+ 2. mv apache-tomcat-8.5.15.tar.gz /usr/local/
+ 3. tar -zxvf apache-tomcat-8.5.15.tar.gz
+ 4. mv apache-tomcat-8.5.15 tomcat
+ 5. 编辑 vi /usr/local/tomcat/bin/catalina.sh
	+ JAVA_HOME=/usr/lib/jvm/jdk1.8
	+ JAVA_OPTS="-Ddruid.registerToSysProperty=true"
+ 6. 将8080端口添加到防火墙例外并重启
    	+ i. systemctl start firewalld.service
	+ ii. firewall-cmd --zone=public --add-port=8080/tcp --permanent
	+ iii. firewall-cmd --reload
	+ iv. #停止firewall systemctl stop firewalld.service 
	+ #禁止firewall开机启动 systemctl disable firewalld.service
+ 7. tomcat 启动巨慢的解决方法
	+ i. 安装熵服务 yum install rng-tools 
	+ ii. 启动熵服务 systemctl start rngd
	+ iii. 熵服务状态 systemctl status rngd
	+ iv. 重新载入服务 
	+ systemctl daemon-reload
	+ systemctl restart rngd
