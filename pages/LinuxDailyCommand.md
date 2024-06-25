<div align='center'>

# Linux Daily Command
</div>

## General
1. Check Ubunto Version:  `lsb_release -a`
1. Change Directory : `cd`
1. Goto root directory: `cd /`
1. Check file/directory: `ls`
1. Check file/directory with details : `ls -l` Explain: drwxr-xr-x => if exixts d that means ‘directory’, l means link, otherwise means ‘file’.
1. Goto home: `cd /home` (in my laptop- cd irfan).
1. Where I’ m now to check: `pwd`
1. Create a new file: 
    ```bash 
    touch <myfile.txt>
    ```
1. Copy one file to another : 
    ```
    cp <file1.txt> <file2.txt>
    ```
1. Remove file:  `rm file2.txt`
1. Remove Directory: 
    ```
    rm -rf <test_folder>
    ```
1. Move file to folder : mv <myfile.txt> <php/myfile123.txt>
1. Copy file and paste one directory back: 
    ```
    cp myfile123.txt ../fileagain.txt
    ```
1. Create Directory: 
    ```
    mkdir another_dir
    ```
1. PC Shutdwon: `shutdwon now`
1. PC Restart: `sudo shutdwon -r now`

## How to install any software from downloads folder
1. `cd Downloads`
1. `ls`
1. `sudo apt install ./discord-0.0.47.deb`

to install all software in one command : `sudo apt install docker-desktop-4.17.0-amd64.deb  firefox.tmp  microsoft-edge-dev_112.0.1702.3-1_amd64.deb`


## visible `.git` folder in ubuntu
- Open the file manager or terminal on your Ubuntu system

- Navigate to the directory where your Git repository is located.

- Press `Ctrl+H` to show hidden files and folders. This will make the ".git" folder visible in the file manager or terminal

- To hide the hidden files and folders again, press  `Ctrl+H` again.

## Git Clone Related issue
https://stackoverflow.com/questions/68775869/message-support-for-password-authentication-was-removed-please-use-a-personal


## To Give Directory and it’s all files permission access 
`sudo chmod -R a+rwx /path/to/folder` to give permissions to the selected folder and its files.

- To Give Directory and it’s all files permission access 
`sudo chmod -R a+rwx /path/to/folder` to give permissions to the selected folder and its files.

- To change permission access to 0755 or 0644
`chmod 0755 your_file_or_directory`
`chmod 0644 your_file_or_directory`

- To change permission access on Directory-0755 and Files – 0644
`find /path/to/your/project -type d -exec chmod 0755 {} +`
`find /path/to/your/project -type f -exec chmod 0644 {} +`

- /varwww/html file permission access
`sudo chmod 777 /var/www/html -R`

Ref: https://stackoverflow.com/questions/50378664/permission-denied-inside-var-www-html-when-creating-a-website-and-its-files-wi

## Switch PHP Version
- display list
```
  sudo update-alternatives --config php
```

- For Disable
```
 sudo a2dismod php8.2
```
- For Enable

```
sudo a2enmod php7.4
```
- For Start

```
sudo service apache2 restart  
```
or,
```
systemctl restart apache2
```

- ref - https://www.youtube.com/watch?v=Xzs4VLc3iE0

- You can execute the command below to change the version straight away:
```
sudo update-alternatives --set php /usr/bin/php7.4
```

## Uninstall PHP Versions
```
sudo apt-get remove php5.6
```

Also, uninstall all the modules for that version, Run the following command:

```
sudo apt-get remove php5.6-*
```

## How to Start, Stop and Restart Apache Server on Ubuntu
```
sudo systemctl start apache2

sudo systemctl stop apache2

sudo systemctl status apache2

sudo systemctl reload apache2
```

Ref: https://phoenixnap.com/kb/ubuntu-start-stop-restart-apache

## How to Start, Stop and Restart MySQL Server on Ubuntu

```
sudo service mysql start

sudo service mysql stop

sudo service mysql restart

sudo service mysql status
```

## Open Xampp :
```
sudo /opt/lampp/./manager-linux-x64.run
```

## One Command before office work (Xampp purpose)
```
sudo systemctl stop apache2 && sudo service mysql stop && sudo /opt/lampp/./manager-linux-x64.run
```

## XAMPP to Normal
```
sudo systemctl start apache2 && sudo service mysql start
```

## To change root directory to an any directory
To switch to root, then execute the curl command. 
```
sudo -s -H
```
Ref : https://stackoverflow.com/questions/68724464/docker-not-running-ubuntu-20-04

Ref : https://github.com/thecodeholic/php-developer-roadmap


## How to Access any file using terminal :
- <b>To Open :</b> sudo nano /etc/php/8.1/cli/php.ini
- <b>To Search any word :</b> Ctrl + W (and then type the word and press ENTER)
- <b>To Save file :</b> Ctrl + O (fille name will be shown, then press ENTER)
- <b>To Exit from Terminal :</b> Ctrl + X

## To delete a `directory` from www : 
```
1. cd /var/www
2. sudo rm -r your_website_directory
```

## Article
### Xampp Install-
https://itsfoss.com/install-xampp-ubuntu/

### XAMPP htdocs Permission issue and Fix in Ubuntu
https://www.computernetworkingnotes.com/linux-tutorials/xampp-htdocs-permission-issue-and-fix-in-ubuntu.html

### Log File Access:
https://stackoverflow.com/questions/23411520/how-to-fix-error-laravel-log-could-not-be-opened