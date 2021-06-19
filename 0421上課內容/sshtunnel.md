# sshtunnel

## 本地埠號轉發，遠端埠號轉發，動態埠號轉發  
  
開3~4台虛擬機，一共三張網卡，增加第三張網卡內部網路名稱叫a
  
### 步驟  
1. 第三張內部網路網卡沒有ip，所以要手動設ip：ip addr add 192.168.1.1/24 brd + dev enp0s9。第二台機器設192.168.1.2/24。ping 192.168.1.1看能不能通。  
2. 第二台機器(伺服器)輸入指令：python -m SimpleHTTPServer 80。第一台機器(客戶端)輸入：curl 192.168.1.2看有沒有抓到網頁  
3. 第一台機器安裝：yum install wireshark-* 。輸入wireshark打開，在enp0s9抓封包，curl 192.168.1.2，可以從wireshark看到封包
