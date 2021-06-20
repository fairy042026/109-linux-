# zabbix使用
  
觀察cpu負載，在虛擬機使用python讓他一直跑  
![image](https://github.com/fairy042026/109-linux-/blob/main/0609%E4%B8%8A%E8%AA%B2%E5%85%A7%E5%AE%B9/photo_2021-06-09_09-42-50.jpg)  
畫面上可以監控到實時數據
![image](https://github.com/fairy042026/109-linux-/blob/main/0609%E4%B8%8A%E8%AA%B2%E5%85%A7%E5%AE%B9/0702.PNG)  
網路流量
![image](https://github.com/fairy042026/109-linux-/blob/main/0609%E4%B8%8A%E8%AA%B2%E5%85%A7%E5%AE%B9/%E6%93%B7%E5%8F%960609.PNG)  

## 簡單報警
host-item-security，下面有兩個細項，其中一個會檢查etc/passwd檔案有沒有被改過，如果被改過要提出警告。
  
1. 點選etc/passwd，把Update interval改成10s(每十秒監控一次)，然後update
2. 在虛擬機新增一個使用者，useradd mark，再usedel -r mark
3. 到monitoring-dashboard會看到發出警告已經被動過(黃色部分)
![image](https://github.com/fairy042026/109-linux-/blob/main/0609%E4%B8%8A%E8%AA%B2%E5%85%A7%E5%AE%B9/06091.PNG)  

## 新增主機
在一般主機上安裝zabbix-agent，讓zabbix-server監控其他主機
  
1. 再開一台機器，當作要安裝的agent，第二台機器開終端機，執行yum -y install zabbix-agent
2. systemctl start zabbix-agent，systemctl status zabbix-agent，systemctl enable zabbix-agent
3. gedit /etc/zabbix/zabbix_agent.conf，找到Server=ip，ip改成伺服器ip(第一台機器ip)，ServerActive也改伺服器ip，Hostname=改自己機器名字(第二台機器)  
![image](https://github.com/fairy042026/109-linux-/blob/main/0609%E4%B8%8A%E8%AA%B2%E5%85%A7%E5%AE%B9/06093.PNG)  
![image](https://github.com/fairy042026/109-linux-/blob/main/0609%E4%B8%8A%E8%AA%B2%E5%85%A7%E5%AE%B9/06094.PNG)  
![image](https://github.com/fairy042026/109-linux-/blob/main/0609%E4%B8%8A%E8%AA%B2%E5%85%A7%E5%AE%B9/06095.PNG)    
4. 存檔。systemctl restart zabbix-agent  
5. 回到dashboard-configuration-hosts，把監控主機加進來
6. 螢幕右上角create host，填主機名稱。(Group點select，如果都沒有你要的，可以到左上角host group創造想要的名稱，這邊我創了一個webservers)
7. 回到hosts，group選webservers。Agent interfaces的ip address填第二台的ip
8. 先不完成，點左上角templates(下面那個)，填linux選第一個，add
![image](https://github.com/fairy042026/109-linux-/blob/main/0609%E4%B8%8A%E8%AA%B2%E5%85%A7%E5%AE%B9/06092.PNG)  
9. 點一下左下的centos7-1，templates填linux選第一個，add，update
10. 第一台機器systemctl restart zabbix-server，重新整理網頁會看到右邊的ZBX亮綠色(如果亮紅色，去檢查zabbix_agent.conf有沒有錯，確認無誤還是紅色可以重新啟動虛擬機試試看)  
![image](https://github.com/fairy042026/109-linux-/blob/main/0609%E4%B8%8A%E8%AA%B2%E5%85%A7%E5%AE%B9/09066.PNG)  

## 監控主機
監控自己想要的指標，可以寫一個監控腳本，判斷指標是否正確，ex:判斷系統目前人數  
  
1. 第二台機器編輯檔案gedit /etc/zabbixzabbix_agentd.conf &
2. 找到UserParameter，新增UserParameter=check_users, who | wc -l
![image](https://github.com/fairy042026/109-linux-/blob/main/0609%E4%B8%8A%E8%AA%B2%E5%85%A7%E5%AE%B9/09088.PNG)  
3. 存檔。systemctl restart zabbix-agent  
