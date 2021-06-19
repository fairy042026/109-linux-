# sshtunnel

## 本地埠號轉發，遠端埠號轉發，動態埠號轉發  
  
開3~4台虛擬機，一共三張網卡，增加第三張網卡內部網路名稱叫a  
![image](https://github.com/fairy042026/109-linux-/blob/main/0421%E4%B8%8A%E8%AA%B2%E5%85%A7%E5%AE%B9/355975.jpg)    
### 步驟(http)  
1. 第三張內部網路網卡沒有ip，所以要手動設ip：ip addr add 192.168.1.1/24 brd + dev enp0s9。第二台機器設192.168.1.2/24。ping 192.168.1.1看能不能通。  
2. 第二台機器(伺服器)輸入指令：python -m SimpleHTTPServer 80。第一台機器(客戶端)輸入：curl 192.168.1.2看有沒有抓到網頁  
3. 第一台機器安裝：yum install wireshark-* 。輸入wireshark打開，在enp0s9抓封包，curl 192.168.1.2，可以從wireshark看到封包。  
**安全性差，而且要有憑證，要買**

### 步驟(ssh)
1. 在第二台機器輸入systemctl status sshd確保ssh有開啟
2. 在第一台機器輸入ssh -Nf -L 5555:192.168.1.2:80 user@192.168.1.2(建立ssh通道的方法，user是伺服器的帳號，192.168.1.2是伺服器ip)  
3. 輸入密碼，之後把瀏覽器打開，輸入http://127.0.0.1:5555
4. 在第二台機器echo hi > hi.htm，第一台機器輸入http://127.0.0.1:5555/hi.htm 。存取本地端的ip及埠號，實際上連結到伺服器端  
![image](https://github.com/fairy042026/109-linux-/blob/main/0421%E4%B8%8A%E8%AA%B2%E5%85%A7%E5%AE%B9/photo_2021-04-21_10-10-25.jpg)  

