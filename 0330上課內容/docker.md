# docker  

docker安裝請參考：https://github.com/fairy042026/docker/blob/master/0915%E4%B8%8A%E8%AA%B2%E5%85%A7%E5%AE%B9.md  
## 

下載不同docker鏡像，上dockerhub搜尋ubuntu(或其他想下載的)    
  
先systemctl start docker  
* 輸入指令docker pull ubuntu:16.04/docker pull ubuntu:18.04下載兩個版本  
* 輸入指令docker image可以看到兩個不同鏡像  
* 把鏡像刪除：docker rmi ubuntu:18.04 或是輸入image id前三個字母刪除: docker rmi 8e4  
  
一個docker負責一件事情就好，維護比較簡單  
    
(先下載httpd鏡像)  
* 網頁伺服器啟動：docker run -itd -p 8080:80 httpd:latest  
* 查看目前正在執行的容器：docker ps  
    
docker要持續執行任務，如果他沒有持續執行，當他任務結束他就死掉了  
    
* 顯示包含已經死亡的docker：docker ps -a  
* 清除已經死亡的docker：docker rm af3(容器id的前三個字母)  
* 清除正在啟用的docker，要先暫停docker才能刪：docker stop id，再使用docker rm id  
* 重新啟動docker：docker start id  
* 想直接刪除正在執行的docker(不建議的暴力法)：docker rm -f id  
* 同一個鏡像產生兩個docker：docker run -itd -p 8080:80 httpd/docker run -itd -p 8081:80 httpd  
  
兩個網站要有各自內容  
* 進去正在執行的容器：docker exec -it id bash  
主機名字跟容器id相同，代表正在容器裡面    
cd htocs/cat index.html/echo "hello" > index.html
開虛擬機瀏覽器，網址列輸入127.0.0.1:8081，或是打開google瀏覽器輸入機器Ip:8080(看你開在哪個埠號)網頁就改了  
![image](https://github.com/fairy042026/109-linux-/blob/main/0330%E4%B8%8A%E8%AA%B2%E5%85%A7%E5%AE%B9/photo_2021-03-30_19-31-32.jpg)  
  
可以進去docker很多次，再開一次終端機，輸入：docker exec -it id bash就進來了，可以從不同終端進入，離開就輸入exit。
若是把原來的容器刪掉，再用同一埠號啟動容器，返回結果不會是原來更改的內容。  
如果已經修改了，希望裡面的內容重新啟動時不會消失，就要把活的容器重新製作成新的鏡像  
* docker exec -it id bash/cd htdocs/echo "hello" > index.html
* docker commit id myhttpd:1.0(給他名稱和標籤)  
* docker images查看新鏡像  
* docker run -itd -p 8082:80 myhttpd:1.0  
  
也可以下載別人的鏡像  
![image](https://github.com/fairy042026/109-linux-/blob/main/0330%E4%B8%8A%E8%AA%B2%E5%85%A7%E5%AE%B9/photo_2021-03-30_20-13-20.jpg)  
  
把鏡像上傳到官網，名字有規定  
* 重新打標籤：docker tag myhttpd:1.0 fairy042026(你的帳號)/myhttpd:1.0  
* 登入docker：docker login，輸入帳號密碼  
* 把鏡像推回去：docker push fairy042026/myhttpd:1.0  
測試鏡像上傳成功，可以先把本地端的刪掉  
* docker rmi id(若有容器正在執行，要先查看正在執行的容器是哪個並刪除)  
* 下載鏡像：docker pull fairy042026/myhttpd:1.0  
* docker run -itd -p 8081:80 fairy042026/myhttpd:1.0  
* curl 127.0.0.1:8081
* 進到ubuntu系統的容器內若想用ping等等的指令，要先apt update，然後再apt install net-tools
