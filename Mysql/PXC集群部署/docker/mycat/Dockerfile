FROM ubuntu:latest

MAINTAINER aquarkgn

# 替换中科大源并更新 apt-get 
RUN sed -i 's/archive.ubuntu.com/mirrors.ustc.edu.cn/g' /etc/apt/sources.list && \
 apt-get update

# 安装 java 服务
RUN apt-get install -y openjdk-8-jdk && \
  echo "export JAVA_HOME=/usr/lib/jvm/java-8-openjdk-amd64" >> /etc/profile && \
  /bin/bash -c "source /etc/profile"

# 安装 mycat 服务
ADD http://dl.mycat.io/1.6.6.1/Mycat-server-1.6.6.1-release-20181031195535-linux.tar.gz /usr/local
RUN cd /usr/local && tar -zxvf Mycat-server-1.6.6.1-release-20181031195535-linux.tar.gz && \
    rm -f Mycat-server-1.6.6.1-release-20181031195535-linux.tar.gz && ls -lna

# 拷贝 mycat 配置文件
COPY conf/rule.xml /usr/local/mycat/conf/
COPY conf/server.xml /usr/local/mycat/conf/
COPY conf/schema.xml /usr/local/mycat/conf/

# 对外开放 8066 9066 端口
EXPOSE 8066
EXPOSE 9066

# 在前台执行 mycat
CMD ["/usr/local/mycat/bin/mycat", "console"]
