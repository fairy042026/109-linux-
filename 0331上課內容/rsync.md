# rsync
## rsync：遠端備份工具
  
rsync+inotify：若駭客入侵，當inotify接收到警告，就觸發rsync覆蓋遠端的資料
  
準備兩台機器  
底層用ssh進行傳輸，免密碼登入  
1. ssh-keygen，一直enter  
2. ssh-copy-id root@ip(另一台機器的ip)  
3. ssh root@ip，確認可以免密碼登入，另一台一樣操作  
  
如何破ssh密碼(John the ripper)  
1. 輸入指令：wget https://packages.endpoint.com/rhel/7/os/x86_64/john-1.8.0-6.ep7.x86_64.rpm  
2. yum install john-1.8.0-6.ep7.x86_64.rpm  
3. cp /etc/shadow shadow.txt
4. john shadow.txt，等了一下就會出現密碼
  
## 安裝rsync+用法
* 安裝：yum install rsync
* 備份
1. mkdir /test -p 
2. mkdir /backup -p
3. cd /test然後touch {1..5}.txt
4. 把test資料夾裡的1~5.txt備份到backup：rsync -avh /test/ /backup(如果test後面沒有加/，代表要把整個test目錄備份過去backup，加上去代表要備份test目錄下的檔案)
   
把本地端的test備份到另一台機器  
* rsync -avzh /test/ root@另一台機器ip:/backup  
另一台機器輸入指令tree /backup就會看到一樣的檔案  
  
從遠端抓回資料  
* rsync -avzh root@另一台機器ip:/backup/ /test  
