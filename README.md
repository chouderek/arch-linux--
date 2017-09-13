# arch-linux-安裝  
舊筆電裝看看arch-linux  
參考arch linux wiki
<https://wiki.archlinux.org/index.php/Installation_guide>  
  

## 1. 安裝前準備  
    [官網下載ISO 安裝映像檔, 然後使用dd指令將iso檔存進USB隨身碟][1]  
      指令： dd bs=4M if=/path/to/archlinux.iso of=/dev/sdx status=progress && sync  

[1]:https://wiki.archlinux.org/index.php/USB_flash_installation_media

## 2. 確認開機模式  
    指令： ls /sys/firmware/efi/efivars  
>若此資料夾不存在，代表就可能是bios開機  
  
## 3. 網路連線  
    若使用wifi上網,要先確認介面名稱。  
    1. 指令：ip link, 確認介面名稱爲wlpxxxxx  
    2. 指令：wifi-menu wlpxxxxx, 連接上網。  
  
## 4. 更新系統時間  
    指令：timedatectl set-ntp true  
  
## 5. 分割硬碟  
      * 指令：fdisk -l, 可以查看硬碟名稱,我的硬碟是/dev/sda1和/dev/sda2
      * 指令：fdisk /dev/sda, 接着要刪除先前的分割表，並建立新的分割表。
      * 接著在fdisk 的command 下, 輸入p查看, d 刪除, n 建立, w 寫入。  
      * 接著使用cfdisk指令, 會有圖形化的分割。
      * 硬碟的分割，我分成/ , /home , swap, 使用cfdisk 分配。
      * 指令：lsblk, 可以查看目前的分割。  
  
## 6. 格式化分割區  
      * 指令：mkfs.ext4 /dev/sda1, for /
      * 指令：mkfs.ext4 /dev/sda3, for /home
      * 指令：mkswap /dev/sda2, for swap
      * 指令：swapon /dev/sda2, 啟動swap  
     
# 7. 掛載
      * 指令：mount /dev/sda1 /mnt
      * 指令：mkdir /mnt/home, mount /dev/sda3 /mnt/home  

# 8. 安裝
      * 指令：vi /etc/pacman.d/mirrorlist, 可以把前面的server取消掉，把臺灣排在第一順位。
      * 指令：pacstrap -i /mnt base base-devel, 開始安裝基本的程式  
  
# 9. 產生fstab  
      * 指令：genfstab -U -p /mnt >> /mnt/etc/fstab, 用genfstab指令產生fstab  
  
# 10. 切換帳號  
      * 指令：arch-chroot /mnt  
  
# 11. 設定語系  
      * 指令： vi /etc/locale.gen,修改把#zh_TW.UTF-8 UTF-8 和#zh_TW BIG5 前面的#拿掉
      * 指令：locale-gen, 重新產生一次語系
      * 指令：echo LANG=en_US.UTF-8 > /etc/locale.conf
      * 指令：export LANG=en_US.UTF-8  
  
# 12. 設定時區  
      * 指令：ln -sf /usr/share/zoneinfo/Asia/Taipei /etc/localtime  
  
# 13. 設定硬體時鐘  
      * 指令：hwclock --systohc --utc  
  
# 14. 設定Hostname  
      * 指令：echo myname > /etc/hostname   
  
# 15. 建立初始的ramdisk環境 
      * 指令：mkinitcpio -p linux  
  
# 16. 先下載無線網路的一些工具  
      * 指令： iw, wpa_supplicant, wireless_tools, dialog  
  
# 17. 設定root密碼  
      * 指令：passwd  
  
# 18. 新增使用者帳號和密碼  
      * 指令：useradd -m -g users -s /bin/bash username
      * 指令：passwd username, 設定密碼  
  
# 19. 建立開機表單  
      * 指令：pacman -S grub-bios, 下載grub
      * 指令：grub-install --target=i386-pc --recheck /dev/sda
      * 指令：cp /usr/share/locale/en\@quot/LC_MESSAGES/grub.mo /boot/grub/locale/en.mo
      * 指令：grub-mkconfig -o /boot/grub/grub.cfg  
  
# 20.安裝結束 
      * 指令：exit
      * 指令：umount /mnt /mnt/home
      * 指令：reboot




