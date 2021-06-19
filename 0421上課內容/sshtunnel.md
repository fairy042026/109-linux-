# sshtunnel

## 本地埠號轉發，遠端埠號轉發，動態埠號轉發  
  
開3~4台虛擬機，一共三張網卡，增加第三張網卡內部網路名稱叫a  
![image](https://github.com/fairy042026/109-linux-/blob/main/0421%E4%B8%8A%E8%AA%B2%E5%85%A7%E5%AE%B9/355975.jpg)    
### 步驟(http)  
1. 第三張內部網路網卡沒有ip，所以要手動設ip：ip addr add 192.168.1.1/24 brd + dev enp0s9。第二台機器設192.168.1.2/24。ping 192.168.1.1看能不能通。  
2. 第二台機器(伺服器)輸入指令：python -m SimpleHTTPServer 80。第一台機器(客戶端)輸入：curl 192.168.1.2看有沒有抓到網頁  
3. 第一台機器安裝：yum install wireshark-* 。輸入wireshark打開，在enp0s9抓封包，curl 192.168.1.2，可以從wireshark看到封包。  
**安全性差，而且要有憑證，要買**  
**如果不想讓人直接連80埠，可以下防火牆規則**  
第二台機器輸入  
![image](https://github.com/fairy042026/109-linux-/blob/main/0421%E4%B8%8A%E8%AA%B2%E5%85%A7%E5%AE%B9/photo_2021-04-21_09-46-47.jpg)  
當輸入192.168.1.2/hi.htm就連不上了  

### 步驟(ssh)
1. 在第二台機器輸入systemctl status sshd確保ssh有開啟
2. 在第一台機器輸入ssh -Nf -L 5555:192.168.1.2:80 user@192.168.1.2(建立ssh通道的方法，user是伺服器的帳號，192.168.1.2是伺服器ip)  
3. 輸入密碼，之後把瀏覽器打開，輸入http://127.0.0.1:5555
4. 在第二台機器echo hi > hi.htm，第一台機器輸入http://127.0.0.1:5555/hi.htm 。存取本地端的ip及埠號，實際上連結到伺服器端  
![image](https://github.com/fairy042026/109-linux-/blob/main/0421%E4%B8%8A%E8%AA%B2%E5%85%A7%E5%AE%B9/photo_2021-04-21_10-10-25.jpg)  

### 三台機器  
情境：翻牆。機器從中國翻牆到台灣的ssh server，這個ssh server可以連到各地的網頁伺服器  
1. 第二台機器(ssh server)再多一張內部網路網卡，名稱叫b。再開第三台機器，三張網卡，第三張內部網路名稱b。
2. 第二台機器確認ssh有沒有開，設定第一張內部網路ip:192.168.1.2/24，第二張ip:192.168.2.2/24。ping 192.168.1.1看能不能ping  
3. 開啟第三台機器，輸入python -m SimpleHTTPServer 80當作網頁伺服器  
4. 第一台機器輸入ssh -Nf -L 5555:192.168.2.1:80 user@192.168.1.2(192.168.2.1是真正要連接的伺服器)  
  
### Remote Port Forwarding
情境：未來在公司裏面辦公，要存取公司的網路，外面的世界沒辦法直接連，所以可以塞一個暗道，連到外面的世界，讓外面反向建一個ssh通道，外面就可以通過通道存取內部資料  
**前面的設定都不改**  
1. 第二台機器輸入echo 1 > /proc/sys/net/ipv4/ip_forward把路由功能打開  
2. 切到第三台機器，ip route show確定有沒有內定路由(default via...)  
3. 切第一台機器，確定可以ping到第三台機器(ping 192.168.2.1)，把網頁伺服器打開python -m SimpleHTTPServer 80
4. 第三台機器當作ssh server把ssh打開  
5. 第一台機器建立反向通道，ssh -Nf -R 192.168.2.1:6666:192.168.1.1:80 user@192.168.2.1(ssh -Nf -R 連的ip是誰:6666:反向連誰的ip:80 user@連的ip是誰)
6. 第三台機器curl 127.0.0.1:6666

  
8. 第二台機器設定防火牆規則
* iptables -A FORWARD -p tcp --destination-port 80 -j DROP
* iptables -A FORWARD -p tcp --destination-port 22 -j ACCEPT
* iptables -A FORWARD -p tcp --destination-port 80 -j DROP
