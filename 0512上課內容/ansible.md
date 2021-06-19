
## ahsible自動化安裝
1. 第二台機器yum remove httpd  
2. 第一台機器建立資料夾example
3. 編輯gedit playbook.yml，內容如下(注意縮排格式一定要對)  
![image](https://github.com/fairy042026/109-linux-/blob/main/0512%E4%B8%8A%E8%AA%B2%E5%85%A7%E5%AE%B9/photo_2021-05-12_10-27-50.jpg)  
4. 第一台機器yum install httpd，cp /etc/httpd/conf/httpd.conf .(拷貝到本地環境下)
5. gedit httpd.conf &，把埠號改8080(Listen 8080)
6. 存檔。ansible-playbook playbook.yml
7. 瀏覽器輸入ip(遠端控制的那台機器ip):8080
![image](https://github.com/fairy042026/109-linux-/blob/main/0512%E4%B8%8A%E8%AA%B2%E5%85%A7%E5%AE%B9/photo_2021-05-12_11-38-07.jpg)  
  
## CentOS 7 下 yum 安装和配置 NFS(安裝伺服器端:第二台，第一台是執行端)  
透過劇本讓伺服器遠端安裝NFS
1. 建立一個資料夾example2，準備兩個檔案exports.j2(配置檔，ip記得改自己的)/playbook.yml(劇本檔)
![image](https://github.com/fairy042026/109-linux-/blob/main/0512%E4%B8%8A%E8%AA%B2%E5%85%A7%E5%AE%B9/photo_2021-05-12_11-27-22.jpg)  
![image](https://github.com/fairy042026/109-linux-/blob/main/0512%E4%B8%8A%E8%AA%B2%E5%85%A7%E5%AE%B9/05121.PNG) 
2. 執行ansible-playbook playbook.yml
3. 到第二台機器，cd /data，systemctl status nfs也在執行
4. 第一台機器showmount -e ip(第二台機器)
5. mkdir /test-nfs。然後mount -t nfs ip(第二台機器):/data /test-nfs
6. cd /test-nfs。touch a b c
7. 切到第二台機器，cd /data也有abc三個檔案
  
## CentOS 7 下 yum 安装和配置 NFS(安裝客戶端:第三台)  
1. 開第三台機器(客戶端機器)，然後第一台機器的playbook.yml檔新增一個server2
![image](https://github.com/fairy042026/109-linux-/blob/main/0512%E4%B8%8A%E8%AA%B2%E5%85%A7%E5%AE%B9/photo_2021-05-12_11-53-15.jpg)  
2. 第一台機器執行ansible-playbook playbook.yml
3. 第三台機器執行ls，可以看到多了/test-nfs資料夾。然後touch 1 2 3
4. 回到第一台cd /data，ls也有123
