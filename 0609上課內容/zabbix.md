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
