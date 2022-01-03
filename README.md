# Development environment bootstrapped by a cloud-config

### Windows

run as root in a newly installed Ubuntu container:
```
export DEBUG_PROC_CMDLINE="ds=nocloud;seedfrom=/mnt/c/Users/username/vm-dev/"
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
