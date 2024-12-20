---
title: Package Management
nav_order: 2
---

# Package Queries &  Management
Package managers like `rpm`, `dpkg` and similar read, update and delete packages from the local package database. On the whole they do not help resolve package dependencies, this is where the subsequent tools, `yum`, `apt` and `apt-get` come in to play.

You can, for example, use `rpm`to install a package and and its dependencies, but you also need to use it to identify those depencies, and which package(s) provide them. 

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

`yum`, `apt` and `apt-get` and similar package management tools help with both package repository management, and package installation with automatic dependency resolution based on additional cached metadata.

| Task  | yum | apt |
|--- |--- |--- |
| List all installed packages | `yum list installed` | `apt list --installed` |
| List all available packages | `yum list available` | `apt list \| grep -v installed` |
| List all installed and available packages | `yum list all` | `apt list` |
| List all installed and available packages for a package | `yum list <packagename>` |  |
| Search for specific packages | `yum search <packagename>` | `apt search <packagename>` |
| Get more info for specific packages | `yum info <packagename>` | `apt info <packagename>` |
| Install a package | `yum install -y <packagename>` | `apt-get -y install <packagename>` |
| Refresh the local version of upstream repository metadata/cache  [1] | `yum makecache` | `apt-get update` |
| Show all applicable updates from upstream repositories | `yum check-update` | `apt-get upgrade -s` (see: `man apt-get`) |
| Update all packages | `yum update -y`  | `apt-get -y upgrade` or `apt-get -y dist-upgrade` |
| Clear local version of upstream repository metadata/cache | `yum clean all` | `apt-get clean` | 
| List all files in a package from the repository [2] | `yum repoquery -l <packagename>` | `apt-file list <packagename>`  |

> **Note [1]:** Yum's default cache expiry is 90 mins so `makecache` is rarely required

> **Note [2]:** `apt-file` is not typically installed by default, it requires `apt-get -y install apt-file` before use

> Note: RHEL 7 and earlier use Yum. RHEL 8 onwards use DNF. Syntax is largely interchangeable.

> Note: DNF moved from 3 -> 4 -> 5. DNF 3 & 4 are Python-based. [DNF5 is C++](https://github.com/rpm-software-management/dnf5/), this includes more rigorous structure for commands/subcommands. As a result certain commands may need more careful ordering but otherwise work as before. 
