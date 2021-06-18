# rsync
## rsync：遠端備份工具
  
rsync+inotify：若駭客入侵，當inotify接收到警告，就觸發rsync覆蓋遠端的資料
  
準備兩台機器  
底層用ssh進行傳輸，免密碼登入  
1. ssh-keygem，一直enter  
2. ssh-copy-id root@ip(另一台機器的ip)  
3. ssh root@ip，確認可以免密碼登入，另一台一樣操作  
  
如何破ssh密碼(John the ripper)  
1. 輸入指令：wget https://packages.endpoint.com/rhel/7/os/x86_64/john-1.8.0-6.ep7.x86_64.rpm  
2. yum install john-1.8.0-6.ep7.x86_64.rpm  
3. cp /etc/shadow shadow.txt
4. john shadow.txt，等了一下就會出現密碼
