---
title: Package Management
nav_order: 2
---

# Package Queries &  Management

| Task  | rpm | dpkg |
|--- |--- |--- |
| List all installed packages | `rpm -qa` | `dpkg --list` |
| List info on an installed package | `rpm -qi <packagename>` | `dpkg --status <packagename>` |
| List all files in an installed package | `rpm -ql <packagename>` | `dpkg --listfiles <packagename>` |
| List key config files in an installed package | `rpm -qc <packagename>` | `cat /var/lib/dpkg/info<packagename>.conffiles`  |
| List key documentation files in an installed package | `rpm -qd <packagename>` |  |
| List installed package that owns the file | `rpm -qf <filepath>` | `dpkg -S <filepath>` |
| List info on a package file | `rpm -qpi <packagename.rpm>` | `dpkg --info <packagename.deb>` |
| List all files in a package file | `rpm -qpl <packagename.rpm>` | `dpkg --contents <packagename.deb>` |
| List key config files in a package file | `rpm -qpc <packagename>` |  |
| List key documentation files in a package file | `rpm -qpd <packagename>` |  |


# Repository Queries &  Management

| Task  | yum | apt |
|--- |--- |--- |
| List all installed packages | `yum list installed` | `apt list --installed` |
| List all available packages | `yum list available` | `apt list \| grep -v installed` |
| List all installed and available packages | `yum list all` | `apt list` |
| List all installed and available packages for a package | `yum list <packagename>` |  |
| Search for specific packages | `yum search <packagename>` | `apt search <packagename>` |
| Get more info for specific packages | `yum info <packagename>` | `apt info <packagename>` |
| Install a package | `yum install -y <packagename>` | `apt-get -y install <packagename>` |
| Refresh the local version of upstream repository metadata/cache | `yum makecache` | `apt-get update` |
| Show all applicable updates from upstream repositories | `yum check-update` | `apt-get upgrade -s` (see: `man apt-get`) |
| Update all packages | `yum update -y`  | `apt-get -y upgrade` or `apt-get -y dist-upgrade` |
| Clear local version of upstream repository metadata/cache | `yum clean all` | `apt-get clean` | 
| **Note:** Yum's default cache expiry is 90 mins so `makecache` is rarely required |
| List all files in a package from the repository | `yum repoquery -l <packagename>` | `apt-file list <packagename>`  |
| **Note:** `apt-file` is not typically installed by default, it requires `apt-get -y install apt-file` before use |  
