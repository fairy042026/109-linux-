# DNS Server反向解析

## 反解：輸入IP位址會解析出網域名稱

**因為我之前做實驗的虛擬機壞掉打不開，所以這邊用老師機示範**

1. 兩台DNS Server，第一台叫dns1.a.com，第二台叫dns2.a.com
2. 修改/etc下的named.rfc1912.zones，加上反向解析的部分，ip的位置是由右往左看，儲存。使用指令named-checkconf確認配置文件沒有錯誤     
![image](https://github.com/fairy042026/109-linux-/blob/main/0317%E4%B8%8A%E8%AA%B2%E5%85%A7%E5%AE%B9/photo_2021-03-17_10-06-03.jpg)  
3. 編輯/var/named的56.168.192.in-addr.arpa.zone  
![image](https://github.com/fairy042026/109-linux-/blob/main/0317%E4%B8%8A%E8%AA%B2%E5%85%A7%E5%AE%B9/photo_2021-03-17_10-07-062.jpg)  
4. 存檔。使用指令named-checkzone 56.168.192.in-addr.arpa /var/named/56.168.192.in-addr.arpa.zone檢查反解析設定檔有沒有問題(前面是反向解析設定檔，後面是正向解析設定檔)  
![image](https://github.com/fairy042026/109-linux-/blob/main/0317%E4%B8%8A%E8%AA%B2%E5%85%A7%E5%AE%B9/photo_2021-03-17_10-09-53.jpg)  
5. 使用指令named-checkconf確認配置文件沒有錯誤，然後systemctl restart named  
6. 輸入反向解析查詢的指令nslookup 192.168.56.200 127.0.0.1確認有無解析成功(上面是正向解下面是反向解)  
![image](https://github.com/fairy042026/109-linux-/blob/main/0317%E4%B8%8A%E8%AA%B2%E5%85%A7%E5%AE%B9/photo_2021-03-17_10-47-20.jpg)  


## 主輔同步
1. 把第二台虛擬機(輔)安裝bind。yum install bind。  
2. 修改 /etc/named.conf，加上masterfile-format text;，把配置改成如下  
![image](https://github.com/fairy042026/109-linux-/blob/main/0317%E4%B8%8A%E8%AA%B2%E5%85%A7%E5%AE%B9/%E6%93%B7%E5%8F%963.PNG)  
3. 把dnssec-validation yes;標記掉，下面改dnssec-validation no;  
![image](https://github.com/fairy042026/109-linux-/blob/main/0317%E4%B8%8A%E8%AA%B2%E5%85%A7%E5%AE%B9/%E6%93%B7%E5%8F%964.PNG)  
4. 存檔。使用指令named-checkconf確認配置文件沒有錯誤。檢查第一台機器(主)跟第二台有沒有同步。可以在兩台機器去按電源-設定-detail-date&time，automatic的那兩個打開。  
![image](https://github.com/fairy042026/109-linux-/blob/main/0317%E4%B8%8A%E8%AA%B2%E5%85%A7%E5%AE%B9/%E6%93%B7%E5%8F%965.PNG)  
5. 第二台機器gedit /etc/sysconfig/named，增加兩行如下  
![image](https://github.com/fairy042026/109-linux-/blob/main/0317%E4%B8%8A%E8%AA%B2%E5%85%A7%E5%AE%B9/%E6%93%B7%E5%8F%967.PNG)  

