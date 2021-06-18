# dns應用

## 智能dns：根據來源Ip，回答的結果不同，應用場景多
![image](https://github.com/fairy042026/109-linux-/blob/main/0324%E4%B8%8A%E8%AA%B2%E5%85%A7%E5%AE%B9/0324-1.jpg)  
* acl:控制訪問列表，把ip進行分類，可以是單一ip、很多ip或一個網路，回復根據acl的群組有不同定義  
  
針對相同的網域名稱，兩台機器訪問同一台伺服器，但是回答是不一樣的 
![image](https://github.com/fairy042026/109-linux-/blob/main/0324%E4%B8%8A%E8%AA%B2%E5%85%A7%E5%AE%B9/0324-3.jpg)  

## 步驟
1. 在/etc/var/named下複製兩個上次的a.com.zone檔案，名稱分別是env-test.a.com.zone/env-prod.a.com.zone並編輯(test.zip檔)    
2. 第一台機器問的時候，希望他回復192.168.56.100，第二台機器問的時候，希望他回復192.168.56.200
![image](https://github.com/fairy042026/109-linux-/blob/main/0324%E4%B8%8A%E8%AA%B2%E5%85%A7%E5%AE%B9/03243.PNG)  
![image](https://github.com/fairy042026/109-linux-/blob/main/0324%E4%B8%8A%E8%AA%B2%E5%85%A7%E5%AE%B9/0324-4.jpg)  
3. 開第一台機器，/etc下的named.rfc1912.zones在最上面定義兩個acl  
![image](https://github.com/fairy042026/109-linux-/blob/main/0324%E4%B8%8A%E8%AA%B2%E5%85%A7%E5%AE%B9/03244.PNG)  
4. 把之前的東西先註解，加上view "env-test".../view "env-prod"...  
![image](https://github.com/fairy042026/109-linux-/blob/main/0324%E4%B8%8A%E8%AA%B2%E5%85%A7%E5%AE%B9/03245.PNG)  
![image](https://github.com/fairy042026/109-linux-/blob/main/0324%E4%B8%8A%E8%AA%B2%E5%85%A7%E5%AE%B9/03248.PNG)  
![image](https://github.com/fairy042026/109-linux-/blob/main/0324%E4%B8%8A%E8%AA%B2%E5%85%A7%E5%AE%B9/03246.PNG)  
5. 存檔。使用指令named-checkconf確認配置文件沒有錯誤。再systemctl restart named。再在第一台機器nslookup www.a.com 192.168.56.108(這邊記得用自己機器的ip)
6. 第二台機器nslookup www.a.com 192.168.56.108。第一台回復56.100，第二台回復56.200  
![image](https://github.com/fairy042026/109-linux-/blob/main/0324%E4%B8%8A%E8%AA%B2%E5%85%A7%E5%AE%B9/photo_2021-03-24_10-44-33.jpg)  
不同的人問相同的東西但得到的答案是不同的。

