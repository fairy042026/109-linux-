# zabbix安裝

1. 在虛擬機打開瀏覽器，進入 https://www.zabbix.com/ 網站，點選download，第一步選擇配置如下  
![image](https://github.com/fairy042026/109-linux-/blob/main/0602%E4%B8%8A%E8%AA%B2%E5%85%A7%E5%AE%B9/photo_2021-06-02_10-49-07.jpg)
2. 跟著步驟執行安裝
* rpm -Uvh https://repo.zabbix.com/zabbix/4.0/rhel/7/x86_64/zabbix-release-4.0-2.el7.noarch.rpm
* yum clean all
* yum install zabbix-get
* yum install -y mariadb-server
* systemctl start mariadb
* systemctl enable mariadb
* yum install zabbix-server-mysql zabbix-web-mysql zabbix-agent
* mysql_secure_installation
3. 進入資料庫時，密碼是空白的，所以直接enter(Enter current...)
4. y / passwd:1234 / passwd:1234 / n / n / y / y   
![image](https://github.com/fairy042026/109-linux-/blob/main/0602%E4%B8%8A%E8%AA%B2%E5%85%A7%E5%AE%B9/photo_2021-06-02_11-01-33.jpg)   
