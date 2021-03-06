### How to build docker image
1. base_os 目录下面的dockerfile主要是用来生成pyalgotrade-cn的基础镜像
  * docker build base_os:xx(版本信息) -f base_os/

2. 当前目录下dockerfile主要是生产策略管理前端和后端的镜像
  * docker build potato:xx(版本信息) .

3. 考虑方便社区成员使用和部署，所有功能集中生成一个镜像

### How to deploy potato
1. linux系统的主机上预装docker，docker-compose，python, pip，git等(ubuntu 16.04 LTS为例)
  * 安装docker参考: https://docs.docker.com/engine/installation/linux/docker-ce/ubuntu/#install-docker-ce
  * apt-get install -y python python-pip git
  * pip install docker-compose

3. Github下载potato工程源码，便于参考内部实现
  * git clone https://github.com/Yam-cn/potato.git

4. 创建三个目录用于挂载potato镜像运行产生数据
  * notebook：Jupyter notebook 存储目录
  * stratlib：策略存储目录
  * mongodb： Mongodb存储目录

5. 考虑到本地编译docker镜像比较花费时间，所以编译后的镜像存储于阿里云的docker registry，大家只需要docker pull下来
  * docker pull registry.cn-hangzhou.aliyuncs.com/potato/potato:0.8

6. 运行potato
  * docker-compose yaml文件目录下运行docker-compose up -d

### How to run strategy
1. Mongodb配置CTP账户(potato.ctp_account{userid:"xxxx"，password:"xxxx"，brokerid:"xxxx"，address:"xxxx"，port:"xxxx“})
  * 推荐下载mongodb客户端compass mongodb： https://www.mongodb.com/download-center?jmp=nav#community

2. 主机stratlib目录存放策略文件

3. 运行和监控策略：http://IP:8080

### How to debug
  * 查看运行日志：docker logs xxxx（container id）
  * 查看后台任务运行状态：http://IP:5555

### TODO
  * 根据大家需要日志收集和展示采用ELK（ElasticSearch, Logstash, Kibana），便于日志管理
  * Docker镜像根据需求生成多个，便于分布式部署和扩展
