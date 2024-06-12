
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


# 如何寫 Dockerfile (example02筆記)

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


10.docker run <id值>

訪問 80 端口發現沒有正常運作，為什麼?

因為此指令僅出於文檔目的添加，它實際上沒有任何作用

您應該添加它以清楚地記錄容器將公開那些端口


11.docker ps

查看所有進程

不加上 -a，則只能看到正在運行的進程


12.docker stop <NAME值>

關閉此容器


13.docker run -p 3000:80 <id值>

加上 -p 它代表發布

這使我們夠告訴 Docker 在哪個本地端口下

-p 然後指定要訪問此應用程序的本地端口


# 更改代碼後，重新 build (後面有優雅的解決方法)

映像一旦建立他們時，基本上是鎖定的

映像中的所有內容都是唯讀的，您不能通過簡單的更新代碼來從外部編輯它

您需要重新構建來獲得更改後的代碼，並基本上將所有更新的代碼複製到映像之中


# 基於層的體系結構，每個指令都代表 Dockerfile 中的一層

當您 構建 映像 或 重新構建 映像，只有發生變化的指令，會被重新評估 (revaluate) 

--> Using cache 使用緩存

基於層的體系結構，每個指令都代表 Dockerfile 中的一層

而一個映像只是根據這些不同的指令從多個層構建而成的

此外，映像是唯讀的，這意味著一旦執行了指令並構建了映像，

映像就會被鎖定，其中的代碼無法更改，除非您重新構映像


# 示範 example02 優化

- 優化前

FROM node

WORKDIR /app

COPY . /app

RUN npm install

EXPOSE 80

CMD ["node", "server.js"]


- 優化後

FROM node

WORKDIR /app

COPY package.json /app

RUN npm install

COPY . /app

EXPOSE 80

CMD ["node", "server.js"]


# Managing Images & Containers

在任何 docker 指令上，可以用 --help 查看所有選項


# 指令_進入 attach(附加模式)(預設非attach)   分離(預設)VS連接的容器

docker run -p 3000:80 -d <id值>

docker attach <name值>

docker logs -f <name值>


# 指令_在 附加模式下 重新啟動 一個停止的容器

docker start -a <name值>


# 指令

docker run -i

-i 他允許在 interactive 交互模式下 啟動此容器

但是 通常會結合 -t 結合使用

-t 將會分配一個偽 tty (Allocate a pseudo-TTY)

# -i 結合 -t

將能夠輸入一些內容

這樣容器將偵聽我們的輸入

並且我們還將獲得容器所公開的終端

該終端實際上是我們輸入的設備


# 指令_docker start

docker start <name值>

會讓 docker 在默認情況下以分離模式啟動(不能與容器通信)


# 指令_docker start -a -i

docker start -a -i <name值>

-a 用於偵聽輸出

-i 用於向容器中輸入內容

這裡不用 -t 是因為他被記住了，再我們最初使用 -t 運行容器時


# example03小結

docker build .

docker run -it <id值>

docker stop <NAME值>

docker start -a -i <name值>


# 2_32_指令_docker rm <name值>

docker rm <name值> 刪除容器

docker rm <name值> <name值> <name值> <name值>


# 2_32_指令_docker images

docker images 映像列表


# 2_32_指令 docker rmi <id值>

docker rmi <id值> 刪除映像

docker rmi <id值> <id值> <id值> <id值>

刪除映像要注意：只有當映像不再被任何容器使用時，

才能刪除映像，(包括停止的容器)

如果有一個已停止的容器，則無法刪除該容器正在使用的圖像，您需要先刪除該容器

docker rm 刪除容器


# 2_32_指令_docker image prune

docker image prune 刪除所有未使用的映像


# 2_33_指令_docker run --rm <id值>

--rm 無論何時停止此容器，它都會自動刪除


# 2_33_example02小結

docker run -p 3000:80 -d --rm <id值>

docker stop <name值>

docker ps -a

發現已經刪除

使用 --rm 啟動容器很常見，尤其在 node 伺服器

因為通常只有在代碼更改時才會停止容器，

這也代表需要重新構建映像

因此無論如何都要啟動一個新容器


# 2_34

docker images 映像包含代碼和應用程序環境(檔案很大)

運行的容器實際上沒有那麼大，它只是一個額外的薄層，基本上是命令層添加在圖像之上，

因此，該圖像代碼在運行容器中使用，它不會再被複製一次

容器在映像上構建，並且基於同一映像運行的多個容器將共享映像內的代碼

這就是為什麼映像中的代碼也被鎖定，唯讀容器只能進行更改


# 2_35_指令_docker image inspect <id值>

docker image inspect <id值> 查看映像的詳細資料


# 5_36_指令_docker cp <本地資料夾/.  容器名稱:/指定要將副本複製到的容器內部的路徑>

查看一個容器，在他已經運行的時候向它添加一些東西或者從它提取一些東西

docker cp <資料夾/本地主機項目文件.txt>

docker cp <資料夾/. 容器名稱:/指定要將副本複製到的容器內部的路徑(如果此路徑不存在則將創建)>

它允許您將文件或資料夾複製到正在運行的容器中或複製出正在運行的容器

測試

docker cp testfolder/. <name值>:/test
刪除本地文件
docker cp <name值>:/test testfolder


# 5_37_指令_docker run --name <自定義名稱值>

容器自定義name值

docker run --help

docker run -p 3000:80 -d --rm --name <自定義名稱值> <id值>


# 5_37_指令_docker build -t <name:tag> .

映像命名 1.標籤TAG

映像標籤由兩部分組成 name : tag

例如 node:14

1.映像的實際名稱(REPOSITORY) -> 

2.tag

名稱可以設置映像的通用名稱 - 可以創建一組多個，更專業的映象，例如 node 我們拉入的映象

標記 - 可以定義該映像的更專門的版本

docker build --help

docker build -t <name:tag> .

在 docker images 看到

node:14 已經轉換名稱變成 name:tag


# 5_39_指令_docker push <DockerId/名稱>

cd 到資料夾

docker build -t <DockerId/名稱> .

docker tag <REPOSITORY:TAG> <DockerId/名稱>
docker tag <REPOSITORY:TAG> <DockerId/名稱:TAG>

重命名映像時，是克隆的，不會刪除舊映像

好了之後

docker push <DockerId/名稱>

如果因為權限問題推不上去，

docker login

Username:
Password:

docker logout


docker pull <DockerId/名稱>

docker run <DockerId/名稱>


# 2_47

example04 展示了 刪除容器 ，會清除容器中的所有數據，因為容器整體被清除和刪除

docker run -p 3000:80 -d --rm <id值>

如果我們運行一個新容器，即使它位於同一個映像上，在前一個容器中創建和存儲的所有數據都會丟失

因為該映像是唯讀的

因此，當在容器中生成文件時，

容器不會將此文件寫入映像

它將其寫入其自己的讀寫層，該層添加在頂部

如果容器被刪除，我們只剩下從未更改過的映象

因此，當我們啟動一個新容器時，它將再次以相同的基本文件系統啟動

而不包含可能已在同一映像上執行的前一個容器所做的更改

核心思想 --> 基於同一映像的多個容器彼此完全隔離


# 3_48 Volums 卷

如果我們停止容器並在此後刪除它，則會丟失此文本文件

但是，在容器被刪除時，我們希望保留這些文件，可能是用戶帳戶、用戶提交的產品數據

解決方案 --> Volums 卷

卷幫我們保留數據

卷是主機上的文件夾，不在容器中，也不在映像中

卷是您的主機上的文件夾，在您的計算機上，您讓 Docker 知道，然後映射到 Docker 容器內的文件夾

有點像 Docker 文件夾的 COPY 指令

COPY：只是對您要它複製的路徑和文件進行快照，然後它將這些文件和文件夾複製到映像中，就只有這樣，沒有持續的關係

而卷不同

您可以將容器內部的文件夾連接到容器外部的文件夾，即主機上的文件夾

並且在任一文件夾中所做的更改都將反映在另一個文件夾中

卷允許您持久保存數據

即使關閉容器，卷也會保留並繼續存在














