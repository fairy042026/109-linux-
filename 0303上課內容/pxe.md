# pxe

## 教學步驟

1. 建立一台叫pxe test的虛擬機，類型：Linux;版本：other linux(64bit)，記憶體：2048MB;硬碟：50GB。到設定-系統，把網路和硬碟勾選，其他兩個不選，並把網路放到最上面，如圖。
![image](https://github.com/fairy042026/109-linux-/blob/main/0303%E4%B8%8A%E8%AA%B2%E5%85%A7%E5%AE%B9/%E8%9E%A2%E5%B9%95%E6%93%B7%E5%8F%96%E7%95%AB%E9%9D%A2%20(414).png)  
1. 到設定-網路，選擇一張網卡(內部網路)，命名為a。其他不選，如圖。
![image](https://github.com/fairy042026/109-linux-/blob/main/0303%E4%B8%8A%E8%AA%B2%E5%85%A7%E5%AE%B9/%E8%9E%A2%E5%B9%95%E6%93%B7%E5%8F%96%E7%95%AB%E9%9D%A2%20(416).png)  
1. 建議另一台虛擬機叫centos，到設定-網路設置三張網卡，1.NAT 2.僅限主機 3.內部網路並命名為a，如圖。
![image](https://github.com/fairy042026/109-linux-/blob/main/0303%E4%B8%8A%E8%AA%B2%E5%85%A7%E5%AE%B9/%E8%9E%A2%E5%B9%95%E6%93%B7%E5%8F%96%E7%95%AB%E9%9D%A2%20(415).png)  
1. 啟動虛擬機centos

    輸入指令：  
    1.yum install tftp-server dhcp syslinux vsftpd  
    2.點選第三張網卡，並更改IPV4配置，apply之後記得關掉重開(on-off-on)，ifconfig確認有沒有設定到。  
    ![image](https://github.com/fairy042026/109-linux-/blob/main/0303%E4%B8%8A%E8%AA%B2%E5%85%A7%E5%AE%B9/%E8%9E%A2%E5%B9%95%E6%93%B7%E5%8F%96%E7%95%AB%E9%9D%A2%20(417).png)  
    3.接下來用putty較方便，記得先關掉防火牆及selinux(vim /etc/selinux/config)。  
    4.vim /etc/dhcp/dhcpd.conf，更改檔案內容如下，ifconfig enp0s9確認無誤。  
    ![image](https://github.com/fairy042026/109-linux-/blob/main/0303%E4%B8%8A%E8%AA%B2%E5%85%A7%E5%AE%B9/photo_2021-03-03_09-43-53.jpg)  
    ![image](https://github.com/fairy042026/109-linux-/blob/main/0303%E4%B8%8A%E8%AA%B2%E5%85%A7%E5%AE%B9/photo_2021-03-03_09-44-34.jpg)  
    5.cd /usr/lib/systemd/system，vim tftp.service，更改檔案內容。  
    ![image](https://github.com/fairy042026/109-linux-/blob/main/0303%E4%B8%8A%E8%AA%B2%E5%85%A7%E5%AE%B9/photo_2021-03-03_09-46-23.jpg)  
    6.mkdir /tftpboot，cd /usr/share/syslinux，cp pxelinux.0 menu.c32 memdisk mboot.c32 chain.c32 /tftpboot/，chmod 644 -R /tftpboot，chmod 755 /tftpboot。  
    7.cd /tftpboot，mkdir pxelinux.cfg，mkdir netboot
    8.打開winscp，把iso檔複製到虛擬機
    
    



