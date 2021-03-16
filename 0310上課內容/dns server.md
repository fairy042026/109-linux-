# DNS Server

## 教學內容

**準備兩台虛擬機:7-1,7-2，兩台都開兩張網路卡，分別是NAT以及僅限主機介面卡**  
1. 虛擬機7-1執行yum install bind-utils, yum install bind -y
2. gedit /etc/named.conf &
3. systemctl start named
4. nslookup www.pchome.com.tw 127.0.0.1
5. systemctl restart named



