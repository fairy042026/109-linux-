# rsync
## rsync：遠端備份工具
  
rsync+inotify：若駭客入侵，當inotify接收到警告，就觸發rsync覆蓋遠端的資料
  
準備兩台機器  
底層用ssh進行傳輸，免密碼登入  
1. ssh-keygem，一直enter  
2. ssh-copy-id root@ip(另一台機器的ip)  
3. ssh root@ip，確認可以免密碼登入，另一台一樣操作  
