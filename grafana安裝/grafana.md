# Grafana安裝
參考網站：https://www.itread01.com/content/1544175663.html
1. wget https://s3-us-west-2.amazonaws.com/grafana-releases/release/grafana-5.3.1-1.x86_64.rpm 
2. yum localinstall  grafana-5.3.1-1.x86_64.rpm 
3. systemctl enable grafana-server
4. systemctl start grafana-server
5. 開瀏覽器輸入：http://ip:3000
6. 預設使用者名稱/密碼：admin/admin，第一次進入會要求改密碼
![image](https://github.com/fairy042026/109-linux-/blob/main/grafana%E5%AE%89%E8%A3%9D/0622.PNG)  

# 結合zabbix
  
這邊建議把zabbix和Grafana都安裝最新版本
  
 wget https://dl.grafana.com/oss/release/grafana-7.5.4-1.x86_64.rpm  
 yum localinstall grafana-7.5.4-1.x86_64.rpm  
 yum clean all  
 yum zabbix-get  
  
rpm -Uvh https://repo.zabbix.com/zabbix/5.4/rhel/7/x86_64/zabbix-release-5.4-1.el7.noarch.rpm
(反正就都重裝就對了過程太亂有點忘了)  
安裝完之後到左邊列表的Configuration-plugins
選zabbix並enable，update，完成後到configure-data source點zabbix，會看鄧以下畫面
![image](https://github.com/fairy042026/109-linux-/blob/main/grafana%E5%AE%89%E8%A3%9D/06231.PNG)  
URL寫的是zabbix server的api地址：http://主機ip/zabbix/api_jsonrpc.php 前面IP換成安裝zabbix的主機ip，後面url不變。  
Zabbix API details的用戶名和密碼就是zabbix web的登錄用戶名和密碼，默認是Admin/zabbix。  
完成後，點擊下面的Save&Test，這樣zabbix就匯入完成了。  









參考網站：https://www.itread01.com/content/1544022964.html  
參考網站：https://blog.downager.com/2019/05/29/CentOS-Zabbix-Grafana-%E5%AE%89%E8%A3%9D/  
參考網站：https://blog.downager.com/2019/05/29/CentOS-Zabbix-Grafana-%E5%AE%89%E8%A3%9D/  
參考網站：https://kknews.cc/zh-tw/tech/rlgzazo.html

