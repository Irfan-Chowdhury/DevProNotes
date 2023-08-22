<div align='center'>

# Linux Daily Command
</div>

## General
1. Change Directory : `cd`
2. Goto root directory: `cd /`
3. Check file/directory: `ls`
4. Check file/directory with details : `ls -l` Explain: drwxr-xr-x => if exixts d that means ‘directory’, l means link, otherwise means ‘file’.
5. Goto home: `cd /home` (in my laptop- cd irfan).
6. Where I’ m now to check: `pwd`
7. Create a new file: 
    ```bash 
    touch <myfile.txt>
    ```
8. Copy one file to another : 
    ```
    cp <file1.txt> <file2.txt>
    ```
9. Remove file:  `rm file2.txt`
10. Remove Directory: 
    ```
    rm -rf <test_folder>
    ```
11. Move file to folder : mv <myfile.txt> <php/myfile123.txt>
12. Copy file and paste one directory back: 
    ```
    cp myfile123.txt ../fileagain.txt
    ```
13. Create Directory: 
    ```
    mkdir another_dir
    ```

## visible `.git` folder in ubuntu
- Open the file manager or terminal on your Ubuntu system

- Navigate to the directory where your Git repository is located.

- Press `Ctrl+H` to show hidden files and folders. This will make the ".git" folder visible in the file manager or terminal

- To hide the hidden files and folders again, press  `Ctrl+H` again.

## Git Clone Related issue
https://stackoverflow.com/questions/68775869/message-support-for-password-authentication-was-removed-please-use-a-personal

## /varwww/html file permission access.
sudo chmod 777 /var/www/html -R

## To Give Directory and it’s all files permission access 
`sudo chmod -R a+rwx /path/to/folder` to give permissions to the selected folder and its files.

## Switch PHP Version
- display list
```
  sudo update-alternatives --config php
```

- for disabled
```
 sudo a2dismod php8.2
```
- for enable

```
sudo a2enmod php7.4
```
- for start

```
sudo service apache2 restart  or systemctl restart apache2
```
