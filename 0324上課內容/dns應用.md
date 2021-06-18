# dns應用

## 智能dns：根據來源Ip，回答的結果不同，應用場景多
![image](https://github.com/fairy042026/109-linux-/blob/main/0324%E4%B8%8A%E8%AA%B2%E5%85%A7%E5%AE%B9/0324-1.jpg)  
* acl:控制訪問列表，把ip進行分類，可以是單一ip、很多ip或一個網路，回復根據acl的群組有不同定義  
  
兩台機器訪問同一台伺服器，回答是不一樣的 
![image](https://github.com/fairy042026/109-linux-/blob/main/0324%E4%B8%8A%E8%AA%B2%E5%85%A7%E5%AE%B9/0324-3.jpg)  

## 步驟
1. 在/etc/var/named下複製兩個上次的a.com.zon檔案，名稱分別是env-test.a.com.zone/env-prod.a.com.zone並編輯  
2. 

