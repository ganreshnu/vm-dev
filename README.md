#Developer environment bootstrapped by a cloud-config#

###Windows###

it really helps to update the wsl guest and "reboot" before running cloud-init:
```
apt-get update && apt-get -y upgrade && exit
\> wsl.exe --shutdown
```

then run the following:
```
\> wsl.exe -u root
export DEBUG_PROC_CMDLINE="ds=nocloud-net;s=https://raw.githubusercontent.com/ganreshnu/vm-dev/master/"
cloud-init init --local
cloud-init init
cloud-init modules --mode config
cloud-init modules --mode final
```

