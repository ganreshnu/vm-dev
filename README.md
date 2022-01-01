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
lxc init ubuntu:lts dev
wget -qO - http://raw.githubusercontent.com/ganreshnu/vm-dev/master/user-data | lxc config set dev user.user-data -
lxc config set dev security.nesting=true
lxc start dev
lxc exec dev -- login -f ubuntu
```

### Other
multipass should work fine.
