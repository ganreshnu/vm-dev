# Development Environment

### Windows
Install the Ubuntu image.
```
wsl --install -d Ubuntu
```

Update the image.
```
wsl -d Ubuntu -u root -- sh -c "apt-get -q update && apt-get -q -y upgrade"
wsl --terminate Ubuntu
```

Optionally export/import an updated image in the current directory.
```
wsl --export Ubuntu Ubuntu-Updated.tar
wsl --import <name> "$Env:LOCALAPPDATA\Packages\<name>" Ubuntu-Updated.tar
```

Open a root shell in the updated image.
```
wsl -d Ubuntu -- login -f root
```

Execute cloud-init passing in the local path to this repository.
```
export DEBUG_PROC_CMDLINE="ds=nocloud;seedfrom=/mnt/c/Users/username/vm-dev/"
cloud-init init --local \
  && cloud-init init \
  && cloud-init modules --mode config \
  && cloud-init modules --mode final \
  && exit
```

"Restart" the image and login.
```
wsl --terminate Ubuntu
wsl -d Ubuntu -- login -f ubuntu
```


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
