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
5. mysql -uroot -p，輸入密碼1234
6. create database zabbix character set utf8 collate utf8_bin;(產生一個資料庫zabbix)
7. create user zabbix@localhost identified by 'zabbix';(產生一個使用者zabbix，密碼zabbix)
8. grant all privileges on zabbix.* to zabbix@localhost;(把zabbix使用者設定權限到zabbix資料庫，讓他可以刪改)
9. quit;
10. zcat /usr/share/doc/zabbix-server-mysql*/create.sql.gz | mysql -uzabbix -p zabbix
11. 密碼zabbix
12. 修改設定，gedit /etc/zabbix/zabbix_server.conf，找到DBPassword=password(passwd改zabbix)並存檔。
13. 修改/etc/httpd/conf.d/zabbix.con，找到php_value date.timezone Europe/Riga(Europe/Riga改Asia/Taipei)
14. systemctl restart zabbix-server zabbix-agent httpd
15. systemctl enable zabbix-server zabbix-agent httpd
16. 在外面google瀏覽器輸入ip/zabbix就可以看到畫面
![image](https://github.com/fairy042026/109-linux-/blob/main/0602%E4%B8%8A%E8%AA%B2%E5%85%A7%E5%AE%B9/%E8%9E%A2%E5%B9%95%E6%93%B7%E5%8F%96%E7%95%AB%E9%9D%A2%20(598).png)  
