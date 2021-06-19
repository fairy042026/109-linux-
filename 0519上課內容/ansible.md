# ansible應用
  
三台機器：一個主控端兩個被控端  
  
## notify
用來觸發另外一個事件，，跳到handlers，notify的名字要跟handlers名字一樣  
  
1. 編輯playbook.yml檔    
![image](https://github.com/fairy042026/109-linux-/blob/main/0519%E4%B8%8A%E8%AA%B2%E5%85%A7%E5%AE%B9/photo_2021-05-19_09-26-55.jpg)  
2. httpd.conf檔案的Listen改8081，存檔後執行ansible-playbook playbook.yml   
3. 瀏覽器輸入ip:8081，就可以看到網頁啟動了  
![image](https://github.com/fairy042026/109-linux-/blob/main/0519%E4%B8%8A%E8%AA%B2%E5%85%A7%E5%AE%B9/photo_2021-05-19_10-05-15.jpg)  
  
## 變數(一個劇本)
裝好一個伺服器想換裝別的伺服器，用變數就可以直接取代，把變數內容改變，直接套用原本的，不會寫死，也不用重新寫  
  
* vars：變數
1. 編輯playbook.yml檔   
![image](https://github.com/fairy042026/109-linux-/blob/main/0519%E4%B8%8A%E8%AA%B2%E5%85%A7%E5%AE%B9/0519%E8%AE%8A%E6%95%B8.PNG)
2. 執行ansible-playbook playbook.yml  
![image](https://github.com/fairy042026/109-linux-/blob/main/0519%E4%B8%8A%E8%AA%B2%E5%85%A7%E5%AE%B9/photo_2021-05-19_10-30-45.jpg)  
  
## 讓變數在不同劇本被使用
準備兩個檔案：playbook.yml / vars_public.yml  
playbook.yml  
![image](https://github.com/fairy042026/109-linux-/blob/main/0519%E4%B8%8A%E8%AA%B2%E5%85%A7%E5%AE%B9/05191.PNG)  
vars_public.yml  
![image](https://github.com/fairy042026/109-linux-/blob/main/0519%E4%B8%8A%E8%AA%B2%E5%85%A7%E5%AE%B9/05192.PNG)  
執行ansible-playbook playbook.yml  
![image](https://github.com/fairy042026/109-linux-/blob/main/0519%E4%B8%8A%E8%AA%B2%E5%85%A7%E5%AE%B9/photo_2021-05-19_10-52-30.jpg)  
  
## 
設定兩個資料夾：group_vars(定義群組變數) / host_vars  
![image](https://github.com/fairy042026/109-linux-/blob/main/0519%E4%B8%8A%E8%AA%B2%E5%85%A7%E5%AE%B9/photo_2021-05-19_10-16-51.jpg)  
