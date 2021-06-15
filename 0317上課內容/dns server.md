# DNS Server反向解析

## 反解：輸入IP位址會解析出網域名稱

**因為我之前做實驗的虛擬機壞掉打不開，所以這邊用老師機示範**

1. 兩台DNS Server，第一台叫dns1.a.com，第二台叫dns2.a.com
2. 修改/etc下的named.rfc1912.zones，加上反向解析的部分
![image](https://github.com/fairy042026/109-linux-/blob/main/0317%E4%B8%8A%E8%AA%B2%E5%85%A7%E5%AE%B9/photo_2021-03-17_10-06-03.jpg)
