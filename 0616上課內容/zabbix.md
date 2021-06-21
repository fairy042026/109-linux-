# Zabbix line noyify

## 報警
假設正常使用者4人，若是大於4就要做報警的動作

1. 把line打開，建立一個群組
2. 開虛擬機，gedit line_notify.sh &(或用putty-vim line_notify.sh)  
3. 把以下內容複製貼上  
![image](https://github.com/fairy042026/109-linux-/blob/main/0616%E4%B8%8A%E8%AA%B2%E5%85%A7%E5%AE%B9/06162.PNG)  
4. 把line_notify.sh變成可執行檔，chmod +x line_notify.sh
5. 到line的環境申請，開啟 https://notify-bot.line.me/zh_TW/
6. 登入，點名字，選取個人頁面-發行權杖-權杖名稱:zabbix-test(隨便寫)-選擇接收群組-發行
7. 把權杖複製，回到虛擬機編輯line_notify.sh，把TOKEN="$1"改成自己的TOKEN(TOKEN="jmBiPDYYpabQXWjnP8ICl.....")並儲存。
8. 執行./line_notify.sh test test "hello world"
