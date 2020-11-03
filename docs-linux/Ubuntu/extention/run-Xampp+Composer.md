# XAMPP Install-Install
Clik Link | <a href="https://www.apachefriends.org/index.html">Visit</a>

## Open directory where file downloads XAMPP and configurasi Install
```
sudo chmod +x xampp-installer.run
./xampp-installer.run
sudo ln -s /opt/lampp/lampp /usr/local/bin/lampp
```
# Composer Install + configurasi Xampp
Downloads Composer at directory ~/Downloads
```
sudo curl -s https://getcomposer.org/installer | /opt/lampp/bin/php
```
Move to directory /usr/local/bin/
```
sudo mv composer.phar /usr/local/bin/composer
```
Create symlink php to /usr/local/bin/
```
sudo ln -s /opt/lampp/bin/php /usr/local/bin/php
```

# XAMPP Desktop Shortcut ?
```
gedit ~/Desktop/xampp-control-panel.desktop
```
```
sudo gedit /usr/share/applications/xampp-control-panel.desktop
```
```
[Desktop Entry]
Encoding=UTF-8
Name=XAMPP Control Panel
Comment=Start and Stop XAMPP
Exec=gksudo /opt/lampp/manager-linux-x64.run
Icon=/opt/lampp/htdocs/favicon.ico
Categories=Application
Type=Application
```
```
chmod +x pathfileyou/xampp-control-panel.desktop
```
