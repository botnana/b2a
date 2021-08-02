## USB 隨身碟掛載

* **在插入 USB 隨身碟前先使用 `fdisk -l `或是 `lsblk` 查看系統目前所能識別的儲存裝置。內容可能如下：**

```
debian@arm:~$ sudo fdisk -l

Disk /dev/mmcblk0: 3.6 GiB, 3867148288 bytes, 7553024 sectors
Units: sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes
Disklabel type: dos
Disk identifier: 0xe67298e5

Device         Boot  Start     End Sectors  Size Id Type
/dev/mmcblk0p1 *      2048  206847  204800  100M  e W95 FAT16 (LBA)
/dev/mmcblk0p2      206848 7553023 7346176  3.5G 83 Linux

Disk /dev/mmcblk0boot1: 2 MiB, 2097152 bytes, 4096 sectors
Units: sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes
Disk /dev/mmcblk0boot0: 2 MiB, 2097152 bytes, 4096 sectors
Units: sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes
```
* **插入 USB 隨身碟，再次使用 `fdisk -l `，查看新增的儲存裝置。與第一次內容相比，新增的內容可能如下，由此內容可以得知新增的儲存裝置代號是 `/dev/sda1`。**

```
Disklabel type: dos
Disk identifier: 0x0009fbbc

Device     Boot Start       End   Sectors  Size Id Type
/dev/sda1  *     2048 121110527 121108480 57.8G  7 HPFS/NTFS/exFAT

```

* **掛載指令，以儲存裝置代號是 `/dev/sda1` 為範例。**

```
debian@arm:~$ sudo mkdir /mnt/usb
debian@arm:~$ sudo mount /dev/sda1 /mnt/usb 
```
* **掛載後就可以在 /mnt/usb 的目錄下對 USB 隨身碟的資料進行訪問或是操作。**
* **卸載指令，以儲存裝置代號是 `/dev/sda1` 為範例。**
```
debian@arm:~$ sudo unmount /dev/sda1 
```

## MicroSD Card 掛載

掛載的方式與 USB 類似，也是由 `fdisk -l` 指令找出掛載的磁碟名稱。

* **`fdisk -l` 查詢後的範例如下：**

```
Disklabel type: dos
Disk identifier: 0x003a8823

Device         Boot Start      End  Sectors  Size Id Type
/dev/mmcblk1p1 *     2048 62333951 62331904 29.7G  c W95 FAT32 (LBA)
```

* **掛載指令，以儲存裝置代號是 `/dev/mmcblk1p1` 為範例。**

```
debian@arm:~$ sudo mkdir /mnt/mmc
debian@arm:~$ sudo mount /dev/mmcblk1p1 /mnt/mmc 
```
* **掛載後就可以在 /mnt/mmc 的目錄下對 MicroSD Card 的資料進行訪問或是操作。**
* **卸載指令，以儲存裝置代號是 ```/dev/mmcblk1p1```為範例。**

```
debian@arm:~$ sudo unmount /dev/mmcblk1p1 
```

**注意事項：**

BN-A2A/BN-B2A 預設會以 MicroSD Card 開機，如果只是資料的訪問或是操作，建議在開機後再插入 MicroSD Card。
 