# arch-linux-安裝  
舊筆電裝看看arch-linux  
參考arch linux wiki
<https://wiki.archlinux.org/index.php/Installation_guide>  
  

## 1. 安裝前準備  
    *_**[官網下載ISO 安裝映像檔, 然後使用dd指令將iso檔存進USB隨身碟][1]**_  
      指令： dd bs=4M if=/path/to/archlinux.iso of=/dev/sdx status=progress && sync  

[1]:https://wiki.archlinux.org/index.php/USB_flash_installation_media

## 2. 確認開機模式  
    指令： ls /sys/firmware/efi/efivars  
>若此資料夾不存在，代表就可能是bios開機  
  
## 3. 網路連線  
    若使用_**wifi**_上網,要先確認介面名稱。  
    1. 指令：ip link, 確認介面名稱爲wlpxxxxx  
    2. 指令：wifi-menu wlpxxxxx, 連接上網。  
  
## 4. 更新系統時間  
    指令：timedatectl set-ntp true  
  
## 5. 分割硬碟  
      * 指令：**fdisk -l**, 可以查看硬碟名稱,我的硬碟是/dev/sda1和/dev/sda2
      * 指令：**fdisk /dev/sda, 接着要刪除先前的分割表，並建立新的分割表。
      * 接著在fdisk 的command 下, 輸入p查看, d 刪除, n 建立, w 寫入。  
      * 接著使用cfdisk 指令, 會有圖形化的分割。
      *


