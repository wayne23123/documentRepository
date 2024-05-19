
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

docker run -it node
我們希望將容器內部的交互式會話公開給我們的宿主計算機
打完後：
進入交互式node終端


通常會建立在這些映像上，然後建立自己的映象


# 指令_列出所有運行中的容器container
docker ps -a
ps 代表進程
-a 將顯示 Docker 為我們創建的所有容器的所有進程


# 如何寫 Dockerfile

1.FROM node
FROM 允許您在另一個基礎映像上構建映像

下一步要告訴 Docker 本地計算機上得那些文件應放入映像中


4.WORKDIR /app

告訴 DOcker 所有後續命令都將從該文件夾中執行


2.COPY . /app

第一個：是容器之外的路徑，即文件應該複製到映像中的映像之外的路徑

寫一個 . 代表：告訴 Docker 他是包含 Docker 文件的同一個文件夾，該項目中的所有文件夾、子文件夾、文件都應複製到 DMH 中

第二個：是映像中的路徑，這些文件應該儲存在其中

每個映像以及基於映像創建的每個容器都有自己的內部文件系統，該文件系統與您的計算機上的文件系統完全分離，它藏在 Docker 的 容器 中

實際上，最好不要用根文件夾，即 Docker 容器的根條目，而是用完全由您決定的某個子文件夾

--> 現在，與 Dockerfile 位於同一文件夾中的所有文件以及所有子文件夾都將被複製到容器內的應用程序文件夾中，
    如果該文件夾不存在，則會在映像和容器中創建該文件夾

5.COPY . ./

教了簡寫，此相對路徑指向 /app


3.RUN npm install

要做 npm install

告訴 Docker 在把所有本地文件複製到鏡像中之後，要在鏡像中運行一個命令

默認在 Docker 容器和映像的工作目錄中執行

默認該工作目錄是該容器文件系統中的根文件夾


8.EXPOSE 80

讓 Docker 知道，當容器啟動時，我們希望向本地系統公開某個端口

我們就可以在這個端口上運行我們監聽的容器


6.RUN node server.js

當所有指令完成後，要重啟服務器

--> 記住，映像應該是容器的模板

    映像不是您最終運行的東西，您運行一個基於映像的容器


7.CMD ["node", "server.js"]

不用上面的 6. 指令了

CMD 和 RUN 差別在於

CMD 不會在創建映像時執行，而是在基於映像啟動容器時執行

CMD 語法，array，用字串分割命令


9.docker build .

在創建好 Dockerfile 之後，到 cmd 打這個指令

想根據這個 Dockerfile 中的指令創建一個映像，告訴 Docker 基於 Dockerfile 構建一個新的自定義映像

這裡需要指定 Docker 能夠找到 Dockerfile 的路徑

後面補上 . 將告訴 Docker，Dockerfile 將位於我們運行此命令的同一個文件夾中

