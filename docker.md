
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


# 指令_停止並關閉容器
docker stop <NAMES值>