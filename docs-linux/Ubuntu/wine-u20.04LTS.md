# How to Install Wine on Ubuntu 20.04 LTS
The procedure on this page installs the latest version of Wine Stable, Wine Development, or Wine Staging.

## Check installed architectures
Verify 64-bit architecture. The following command should respond with "amd64".
```
$ dpkg --print-architecture
```
See if 32-bit architecture is installed. The following command should respond with "i386".
```
$ dpkg --print-foreign-architectures
```
If "i386" is not displayed, execute the following.
```
$ sudo dpkg --add-architecture i386
```
Recheck with.
```
$ dpkg --print-foreign-architectures
```
Add the WineHQ Ubuntu repository.
Get and install the repository key.
```
$ wget -nc https://dl.winehq.org/wine-builds/winehq.key
$ sudo apt-key add winehq.key
```
Add the repository.
```
$ sudo add-apt-repository 'deb https://dl.winehq.org/wine-builds/ubuntu/ focal main'
```
Update the package database.
```
$ sudo apt update
```
Install Wine
The next command will install Wine Stable. If you prefer Wine Development or Wine Staging, replace winehq-stable with either winehq-devel or with winehq-staging.
```
$ sudo apt install --install-recommends winehq-stable
```
Verify the installation succeeded.
```
$ wine --version
```
https://wine.htmlvalidator.com/install-wine-on-ubuntu-20.04.html
