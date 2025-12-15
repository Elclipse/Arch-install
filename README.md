# Arch-install

# This guide is for efi mode only

Connecting to the internet

  For ethernet
  
```
Auto connect
```

  For wifi

```
iwctl
device list
station [device name] scan
station [device name] get-networks
station [device name] connect [your wifi name] >> input your password
exit
```

Set up partition
```
cfdisk > choose gpt
```
  First creat a boot partition 
```
for BIOS is: 10MB
for efi is: 500MB
new > 10MB or 500MB> enter
```
  Second creat a swap partition (shound add at least 1GB for swap) (recommend 4GB for swap)
```
new > XG/MB > enter | X is the amount of Gib or MB you want to use for swap
```
  Third creat main partition
```
new > enter
```
  Then Write partition
```
choose write > type yes > enter > quit
```

Make and Mount partition
  Make
```
mkfs.ext4 /dev/sda3
mkfs.fat -F 32 /dev/sda1
mkswap /dev/sda2
```
  Mount
```
mount /dev/sda3 /mnt
mkdir -p /mnt/boot/efi
mount /dev/sda1 /mnt/boot/efi
swapon /dev/sda2
```

Install basic packages
```
pacstrap /mnt base linux linux-firmware sof-firmware base-devel grub efibootmgr nano networkmanager
```

Generate fstab
```
genfstab /mnt > /mnt/etc/fstab
```

Change to root user
```
arch-chroot /mnt
```

Setting timezone
```
ln -sf /usr/share/zoneinfo/your region/your city /etc/localtime
use date check if time is correct and then syncing timezone
hwclock --systohc | this will sync your timezone
```

Setting localization
```
nano /etc/locale.gen
scroll down by using arrow key > find the line "en_US.UTF-8 UTF-8" > delete "#" > press CTRL+S to save > press CTRL+X to exit
locale-gen
nano /etc/locale.conf > type "LANG=en_US.UTF-8" > press CTRL+S to save > press CTRL+X to exit
```

Creating hostname
```
nano /etc/hostname > type your name for your host machine > press CTRL+S to save > press CTRL+X to exit
```

Setting up root password
```
passwd > type your password for your root user
```

Add user
```
useradd -m -G wheel -s /bin/bash [your user name]
passwd [your user name] | set password for your user
```

Add your user to sudo
```
EDITOR=nano visudo
fine line "%wheel ALL=(ALL) ALL" at the bottom > delete "#" > press CTRL+S to save > press CTRL+X to exit
```

Creating bootloader
```
grub-install /dev/sda
grub-mkconfig -o /boot/grub/grub.cfg
```

Enable network
```
systemctl enable NetworkManager
```

Reboot the system
```
exit
umount -a | check if all the partition are working
rebott
```

Enable wifi after installation
```
nmcli device wifi list | will list the available wifi networks

nmcli device wifi connect SSID or BSSID password | to connect to a specific wifi networks
```

Install desktop environment:
  Jakoolit arch hyprland script
```
git clone --depth=1 https://github.com/JaKooLit/Arch-Hyprland.git ~/Arch-Hyprland
cd ~/Arch-Hyprland
chmod +x install.sh
./install.sh
```
  Xfce4
```
sudo pacman -S xfce4 xfce4-goodies
sudo pacman -S lightdm lightdm-gtk-greeter
sudo systemctl enable lightdm.service
```
  KDE Plasma
```
sudo pacman -S plasma
sudo pacman -S sddm
sudo systemctl enable sddm
```

Install unikey 
```
sudo pacman -S fcitx5 fcitx5-qt fcitx5-unikey kcm-fcitx5
 > go to hyprland conf file
type comment "exec fcitx5"  > save
```
