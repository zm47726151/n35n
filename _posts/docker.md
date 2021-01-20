### 启动docker

​	systemctl start docker

### 配置开机启动docker

​	sudo systemctl enable docker

### 启动nexus

​	docker run -tid -p 8081:8081 --name nexus -e NEXUS_CONTEXT=nexus -v /usr/local/nexus3/nexus-data:/nexus-data  docker.io/sonatype/nexus3

### 安装Jenkins

​	拉取镜像
​	docker pull jenkins/jenkins:lts
​	运行jenkins容器
​	docker run -d --restart=always --name=jenkins -p 3000:8080 -p 50000:50000 -v $PWD:/opt/jenkins -v /var/run/docker.sock:/var/run/docker.sock -v /usr/bin/docker:/usr/bin/docker --env JENKINS_OPTS='--prefix=/jenkins' jenkins/jenkins:lts
​	查看日志
​	docker logs -f jenkins
​	进入jenkins容器
​	docker exec -it jenkins /bin/bash
​	

### 安装minio

​	docker run -p 9000:9000 --name minio \
​	-d --restart=always \
​	-e "MINIO_ACCESS_KEY=admin" \
​	-e "MINIO_SECRET_KEY=admin123456" \
​	-v /home/data:/data \
​	-v /home/config:/root/.minio \
​	minio/minio server /data
​	
docker 同步宿机时间到容器（zoo2）时间
​	docker cp /usr/share/zoneinfo/Asia/Shanghai zoo2:/etc/localtime	
docker设置开机启动
​	docker update --restart=always mysql
启动mysql
docker start mysql
