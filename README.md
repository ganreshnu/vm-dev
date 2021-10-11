# Development environment bootstrapped by a cloud-config

### Windows
it really helps to update the wsl guest and "reboot" before running cloud-init:
```
wsl.exe -u root -- sh -c "apt-get update && apt-get -y upgrade"
wsl.exe --shutdown
```

then run the following as root in the container:
```
export DEBUG_PROC_CMDLINE="ds=nocloud-net;s=https://raw.githubusercontent.com/ganreshnu/vm-dev/master/"
cloud-init init --local \
  && cloud-init init \
  && cloud-init modules --mode config \
  && cloud-init modules --mode final \
  && exit
```
use the container with `wsl.exe -u ubuntu`.

### Linux
```
lxc launch -c user.user-data="$(wget -qO - https://raw.githubusercontent.com/ganreshnu/vm-dev/master/user-data)" ubuntu:lts dev
lxc config device add dev home disk source=$HOME path=/mnt/Home
lxc config set dev raw.idmap "both 1000 1000"
lxc restart dev
lxc exec dev -- login -f ubuntu
```

### Other
multipass should work fine.
