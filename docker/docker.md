
https://docs.docker.com/


windows 10 hyper v


安裝


安裝好後到 cmd 第一個指令 
docker


沒報錯代表安裝成功


Docker Desktop


# 指令_構建 Docker 文件的映象
docker build .

得到 id
writing image sha256:701327d64ab21272207409e6d7d8cf1cd95e478418999b9b1116abebfe2a460c


# 指令_
docker run <id值>



# 第一個 example 有 EXPOSE 3000
 docker run -p 3000:3000 <id值>

 瀏覽器到 http://localhost:3000/ 即可以訪問


# 指令_列出所有運行中的容器container
docker ps

注意STATUS看有無運作


# 指令_停止並關閉容器
docker stop <NAMES值>


# Container VS Images

Container - The running 'unit of software'

Image - Template for containers

映像 - 包含所有設置說明和所有代碼的可共享軟件包

容器 - 映像的具體運行實例


# docker_hub
https://hub.docker.com/



docker run node
使用在 Docker hub 上找到的 節點 映像，來創建容器


# 指令_
docker ps -a
ps 代表進程
-a 將顯示 Docker 為我們創建的所有容器的所有進程
