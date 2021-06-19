# ansible自動化運作維護管理工具
假設管理好幾千台機器，可以自動化管理，讓他自動化安裝軟體，自動化配置，自動化啟動服務，拷貝
  
這邊用老師機做示範  
本地端先免密碼登入，第二、三台一樣  
  
第一台機器安裝：yum install ansible  
確認版本：ansible --version  

主機清單Ansible inventory：針對機器進行分類，管理伺服器的時候，可能要管理很多不同伺服器，就要分門別類進行管理
cd /etc/ansible/
gedit hosts & 編輯內容，新增主機清單如下(第二、三台主機ip)
![image](0428-1)
存檔。執行：ansible webservers -a "hostname"(webserver要執行的清單，hostname要查詢的主機名字)  
![image](0428-2)

執行時出現顏色
* 黃色：對遠端節點進行相應修改
* 綠色：對遠端節點不進行相應修改，或者只是對遠端節點資訊進行查看
* 紅色：操作執行命令有異常
* 紫色：表示對命令執行發出警告資訊（可能存在的問題，給你一下建議）

ansible指令模塊
* command命令模塊
* script腳本模塊
* yum安裝軟體模塊
* copy文件拷貝模塊
* file文件配置模塊
* service服務模塊

看我們要做什麼事，寫好主機清單，這些指令會發送到對應的主機做對應的事

* ansible -doc -l：顯示模塊
* ansible server2 -m yum -a "name=httpd state=absent"：移除httpd  
* ansible server2 -m yum -a "name=httpd,vsftpd state=latest"：一次安裝多個軟體 
* ansible server2 -m shell -a "ifconfig | grep enp0s3" ：執行複雜動作(command做不來的時候)

腳本內容：      
了解其他機器的enp0s3 ip設定，並放到遠端執行。準備一個檔案showip.sh  
  
#!/usr/bin/bash  
  
ip=`ifconfig enp0s3 | grep inet | grep -v inet6 | awk '{print $2}'`  
  
echo $ip  
  
輸入指令：ansible webservers -m script -a "./showip.sh"  
  
* ansible server2 -m copy -a "src=./httpd.conf dest=/tmp/a.conf"(a.conf是改名稱)：拷貝  
* ansible server2 -m copy -a "src=./httpd.conf dest=/tmp/a.conf backup=yes"：備份  
* ansible server2 -m copy -a "content='this is an apple. 'dest=/tmp/b.txt"：裡面的內容想自己打進去而非來自某個檔案  
* ansible server2 -m copy -a "content='this is an apple.'dest=/tmp/b.txt owner=user group=user mode=666"：拷貝過去的時候更改擁有者&群組&權限  
* ansible server2 -m file -a "path=/tmp/aaa state=directory"：在tmp資料夾下新增一個資料夾aaa
* ansible server2 -m file -a "path=/tmp/bbb state=touch owner=user group=user mode=666"：新增一個檔案bbb，並更改擁有者&群組&權限
* ansible server2 -m file -a "path=/tmp/aaa state=directory owner=user group=user recures=yes"：把整個目錄屬性全改
* ansible server2 -m file -a "path=/tmp/bbb state=absent"：檔案bbb刪除
