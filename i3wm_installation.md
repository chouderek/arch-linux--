# i3wm 安裝 &  建置

## Xorg 安裝
要有圖形顯示,要先裝X server  
*指令：pacman -S xorg
*指令：pacman -S xorg-xinit
*在$HOME新增一個.xinitrc, 然後執行echo > exec i3

## i3wm視窗管理器安裝
1.指令:pacman -S i3, i3status, i3blocks, dmenu, i3lock

## 安裝vim
1.指令：pacman -S vim

## 安裝看圖軟體feh
1. 指令：pacman -S feh

>執行startx, 就會進入i3視窗環境。
