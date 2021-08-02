## USB連線IP設定

### 同一電腦連接單一塊 Botnana
* 編輯 Botnana 系統的 /etc/network/interfaces 檔案，改成您所希望的 IP，例如︰

    iface usb0 inet static  

        address 192.168.6.2  

        netmask 255.255.255.0  

        network 192.168.6.0  

        gateway 192.168.6.1  


    表示 Botnana 本身的 IP 是 **192.168.6.2**，分配給電腦的 IP 是 **192.168.6.1**

* 編輯 Botnana 的組態檔 /etc/botnana-control/motion.toml，做如下的修改︰  

    [server]  

    address = "0.0.0.0:3012"  

    改成  

    [server]  

    address = "192.168.6.2:3012"  

    表示 Botnana 本身的伺服器的位址為 **192.168.6.2** 


### 同一電腦連接多塊 Botnana  

修改方式如 **同一電腦連接單一塊 Botnana** ，最大的差異是︰**每塊Botnana要設為不同的區段**。

例如︰
第一塊設為 address 192.168.**6**.2，第二塊設為 address 192.168.**7**.2。