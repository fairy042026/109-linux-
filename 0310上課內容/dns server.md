# DNS Server

## 教學內容

**準備兩台虛擬機:7-1,7-2，兩台都開兩張網路卡，分別是NAT以及僅限主機介面卡，開始記得要關防火牆以及selinux，這邊是用老師機做示範**  

### 第一個實驗  
1. 虛擬機7-1執行yum install bind-utils, yum install bind -y
2. gedit /etc/named.conf & 會看到如下畫面  
![image](https://github.com/fairy042026/109-linux-/blob/main/0310%E4%B8%8A%E8%AA%B2%E5%85%A7%E5%AE%B9/%E8%9E%A2%E5%B9%95%E6%93%B7%E5%8F%96%E7%95%AB%E9%9D%A2%20(426).png)
3. systemctl start named
4. nslookup www.pchome.com.tw 127.0.0.1 (沒有成功記得restart named)   
![image](https://github.com/fairy042026/109-linux-/blob/main/0310%E4%B8%8A%E8%AA%B2%E5%85%A7%E5%AE%B9/%E8%9E%A2%E5%B9%95%E6%93%B7%E5%8F%96%E7%95%AB%E9%9D%A2%20(428).png)
5. 切到虛擬機7-2，為了要讓7-2可以連到7-1，需要改掉7-1的 /etc/named.conf的127.0.0.1以及localhost，改成any  
![image](https://github.com/fairy042026/109-linux-/blob/main/0310%E4%B8%8A%E8%AA%B2%E5%85%A7%E5%AE%B9/%E8%9E%A2%E5%B9%95%E6%93%B7%E5%8F%96%E7%95%AB%E9%9D%A2%20(430).png)  
6. systemctl restart named 
7. 7-2虛擬機執行host -t a www.pchome.com.tw 192.168.56.108(7-1老師機 ip)  
![image](https://github.com/fairy042026/109-linux-/blob/main/0310%E4%B8%8A%E8%AA%B2%E5%85%A7%E5%AE%B9/%E8%9E%A2%E5%B9%95%E6%93%B7%E5%8F%96%E7%95%AB%E9%9D%A2%20(432).png)
8. 切到7-1，使用指令named-checkconf確認配置文件沒有錯誤
9. vim /etc/resolv.conf ，增加一個nameserver 192.168.56.108(7-1老師機 ip，也就是自己ip位址)，儲存後可以用host -t a www.pchome.com.tw 看能不能解析出來

### 第二個實驗-管理網路 

**一樣準備兩台虛擬機，這邊是用自己的實驗做示範**  
1. 打開vm2，gedit /etc/named.rfc1912.zones在最下面新增一個網域  
![image](https://github.com/fairy042026/109-linux-/blob/main/0310%E4%B8%8A%E8%AA%B2%E5%85%A7%E5%AE%B9/%E8%9E%A2%E5%B9%95%E6%93%B7%E5%8F%96%E7%95%AB%E9%9D%A2%20(443).png)  
2. gedit /var/named/a.com.zone寫入以下資訊  
![image](https://github.com/fairy042026/109-linux-/blob/main/0310%E4%B8%8A%E8%AA%B2%E5%85%A7%E5%AE%B9/%E8%9E%A2%E5%B9%95%E6%93%B7%E5%8F%96%E7%95%AB%E9%9D%A2%20(445).png)  
3. 用指令named-checkzone a.com /var/named/a.com.zone確認無誤  
4. systemctl restart named  
5. 切到vm2 0310，輸入指令host -t a www.a.com.tw 192.168.56.125)，打開cmd，輸入指令nslookup www.a.com.tw 192.168.56.125，看能不能查詢到，有查到代表正解成功  
![image](https://github.com/fairy042026/109-linux-/blob/main/0310%E4%B8%8A%E8%AA%B2%E5%85%A7%E5%AE%B9/%E8%9E%A2%E5%B9%95%E6%93%B7%E5%8F%96%E7%95%AB%E9%9D%A2%20(435).png)





