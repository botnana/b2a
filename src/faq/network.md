## 網路設定

使用 `connmanctl` 指令進行設定。以下是幾個常用的設定需求，若是需要詳細說明可參考 [connmanctl - Connman CLI](http://manpages.ubuntu.com/manpages/artful/man1/connmanctl.1.html)
   
### WIFI 設定
    
**查詢無線網卡的狀態**

安裝無線網卡後，使用 `sudo connmanctl technologies` 查詢無線網卡的狀態，
命令輸出後，狀態如下：

```
debian@arm:~$ sudo connmanctl technologies 
[sudo] password for debian: // 輸入 temppwd
/net/connman/technology/wifi
  Name = WiFi
  Type = wifi
  Powered = False
  Connected = False
  Tethering = False
/net/connman/technology/gadget
  Name = Gadget
  Type = gadget
  Powered = False
  Connected = False
  Tethering = False
```

如果無線網卡安裝妥當，應可看到 `/net/connman/technology/wifi` 的資訊，
請注意其中 `Powered = False`， 表示必須先啟動 WiFi，啟動方式如下：

```
debian@arm:~$ sudo connmanctl enable wifi 
Enabled wifi
```

成功後會出現 `Enable wifi` 的訊息。也可再使用 `sudo connmanctl technologies` 確認狀態。

此連線是屬於 DHCP， 如要使用指定IP，請看以下章節。


**開始進行連線設定**

首先進到設定畫面，輸入 `sudo connmanctl`，會出現 `connmanctl>` 等待命令的提示訊息。

```
debian@arm:~$ sudo connmanctl
connmanctl>
```

列出可使用的網路節點，以動程公司為例：

```
connmanctl> services
    Mapacode_5G          wifi_1c5f2bc586d1_4d617061636f64655f3547_managed_psk
    Mapacode             wifi_1c5f2bc586d1_4d617061636f6465_managed_psk
```

開啟連線代理:

```
connmanctl> agent on
Agent registered
```

連線， 以連線到SSID是 Mapacode 為例，


```
connmanctl> connect wifi_1c5f2bc586d1_ //可嘗試按 tab 鍵補全
connmanctl> connect wifi_1c5f2bc586d1_4d617061636f6465_managed_psk 
Agent RequestInput wifi_1c5f2bc586d1_4d617061636f6465_managed_psk
  Passphrase = [ Type=psk, Requirement=mandatory, Alternates=[ WPS ] ]
  WPS = [ Type=wpspin, Requirement=alternate ]
Passphrase? 
```

輸入密碼，等待出現 `Connected wifi_1c5f2bc586d1_4d617061636f6465_managed_psk` 就大功告成。

```
Passphrase? 062970665 // 輸入密碼
Connected wifi_1c5f2bc586d1_4d617061636f6465_managed_psk
connmanctl>  
```

輸入 exit 離開設定畫面

```
connmanctl> exit
debian@arm:~$ 
```

### 有線網路設定

先將網路線連上， 使用 `sudo connmanctl technologies` 查詢連線狀態。應會出現 `/net/connman/technology/ethernet` 項目

```
debian@Q190G4:~$ sudo connmanctl technologies 
[sudo] password for debian: // 輸入 temppwd
/net/connman/technology/ethernet
  Name = Wired
  Type = ethernet
  Powered = True
  Connected = False
  Tethering = False
```

**開始進行連線設定**

首先進到設定畫面，輸入 `sudo connmanctl`，會出現 `connmanctl>` 等待命令的提示訊息。

```
debian@arm:~$ sudo connmanctl
connmanctl>
```

列出可使用的網路節點：

```
connmanctl> services
*A  Wired                ethernet_00ecacce3a79_cable
connmanctl>  
```

開啟連線代理:

```
connmanctl> agent on
Agent registered
```

連線:

```
connmanctl> connect ethernet_00ecacce3a79_cable
Connected ethernet_00ecacce3a79_cable
```

大功告成。

此連線是屬於 DHCP 。如要使用指定IP，請看以下章節。

### 指定IP

設定案例：

* service : `ethernet_00ecacce3a79_cable`
* ip      : 192.168.7.2
* netmask : 255.255.255.0
* gateway : 192.168.7.1


```
指令格式：
connmanctl config <service> --ipv4 manual <ip address> <netmask> <gateway>

案例設定：
sudo connmanctl config  ethernet_00ecacce3a79_cable --ipv4 manual 192.168.7.2 255.255.255.0 192.168.7.1
```

### 自動指派IP

設定案例：

service: `ethernet_00ecacce3a79_cable`


```
指令格式：
connmanctl config <service> --ipv4 dhcp

案例設定：
sudo connmanctl config  ethernet_00ecacce3a79_cable --ipv4 dhcp
```






