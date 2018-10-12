#  vue
使用docker-compose部署vue
## 使用
1. 在linux服务器上安装docker和docker-compose，windows上安装docker需要升级到专业版以上，
    mac上可以使用homebrew命令直接安装brew cask install docker
2. 安装git    
3. clone项目    
 ```
 git clone https://qbanxiaoli@github.com/qbanxiaoli/vue.git 
 ```    
4. 进入vue目录  
```
 cd vue
```   
5. 编译vue项目，生成dist文件夹
```
npm run build
```  
 
6. 执行docker-compose命令构建镜像  
```
docker-compose build
```
7. 执行docker-compose命令后台启动容器  
```
docker-compose up -d
```
8. 测试vue项目是否部署成功，通过ip+宿主机的映射端口进行访问
可以将镜像直接推送到阿里云镜像仓库，再到服务器上拉去镜像后部署
通过jenkins+docker实现容器的自动化部署