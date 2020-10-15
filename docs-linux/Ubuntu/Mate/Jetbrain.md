# Standalone installation﻿
Install PyCharm manually to manage the location of every instance and all the configuration files. For example, if you have a policy that requires specific install locations.

# Install using tar archives﻿
If snap packages are not available, unpack the pycharm-*.tar.gz file to a different folder, if your current Download folder doesn't support file execution:
```
tar xzf pycharm-*.tar.gz -C <new_archive_folder>
```
Copied!
The recommended installation location according to the filesystem hierarchy standard (FHS) is /opt. To install PyCharm into this directory, enter the following command:
```
sudo tar xzf pycharm-*.tar.gz -C /opt/
```
Copied!
To verify integrity of the downloaded archive, use the SHA checksum linked from the Download page.

Switch to the bin subdirectory:
```
cd <new archive folder>/pycharm-*/bin
```
Copied!
For example,
```
cd /opt/pycharm-*/bin
```
Copied!
Run pycharm.sh from the bin subdirectory.
```
sh pycharm.sh
```
Copied!
When you run PyCharm for the first time, some steps are required to complete the installation, customize your instance, and start working with the IDE.

For more information, see Run PyCharm for the first time.

# Create Launc
```
~/.local/share/applications/pycharm.desktop
```
------------------
```
[Desktop Entry]
Encoding=UTF-8
Name=PyCharm
Exec=/opt/pycharm-2020.2.2/bin/pycharm.sh
Icon=/opt/pycharm-2020.2.2/bin/pycharm.png
Type=Application
Categories=Development;IDE;
StartupWMClass=PyCharm
```
