# Arch-install

# This guide is for efi mode only

Connecting to the internet

  ethernet
  
```
ip link
```

  wifi

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
new > 100M > enter
```
  Second creat a swap partition (shound add at least 1GB for swap) (recommend 4GB for swap)
```
new > 1G - 4G > enter
```
  Third creat main partition
```
new > enter
```
Write partition
```
choose write > type yes > enter > quit
```
