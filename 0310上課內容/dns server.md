# DNS Server

## 教學內容

**準備兩台虛擬機:7-1,7-2，兩台都開兩張網路卡，分別是NAT以及僅限主機介面卡**  
1. 虛擬機7-1執行yum install bind-utils, yum install bind -y
2. gedit /etc/named.conf & 會看到如下畫面  
![image](https://github.com/fairy042026/109-linux-/blob/main/0310%E4%B8%8A%E8%AA%B2%E5%85%A7%E5%AE%B9/%E8%9E%A2%E5%B9%95%E6%93%B7%E5%8F%96%E7%95%AB%E9%9D%A2%20(426).png)
3. systemctl start named
4. nslookup www.pchome.com.tw 127.0.0.1  
![image](https://github.com/fairy042026/109-linux-/blob/main/0310%E4%B8%8A%E8%AA%B2%E5%85%A7%E5%AE%B9/%E8%9E%A2%E5%B9%95%E6%93%B7%E5%8F%96%E7%95%AB%E9%9D%A2%20(428).png)
5. systemctl restart named



