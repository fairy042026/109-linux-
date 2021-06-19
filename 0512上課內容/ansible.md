
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
  
## CentOS 7 下 yum 安装和配置 NFS
