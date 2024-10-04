# Arch-install

# This guide is for efi mode only

Connect internet

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

