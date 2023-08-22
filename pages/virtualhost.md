<div>
# Linux Virtualhost Setup

</div>

## Primary Setup

1. Modify the Hosts File
    ```
    sudo nano /etc/hosts
    ```

2. Add the following line to the hosts file
    ```
    127.0.0.1 peopleprosaas.test
    ```
3. Configure the Virtual Host (Apache)
    ```
    sudo nano /etc/apache2/sites-available/peopleprosaas.conf
    ```
4. Add the following configuration to the file
    ```
    <VirtualHost *:80>
        ServerName peoplepro.test
        DocumentRoot /path/to/your/laravel/project/public

        <Directory /path/to/your/laravel/project/public>
            Options Indexes FollowSymLinks
            AllowOverride All
            Require all granted
        </Directory>

        ErrorLog ${APACHE_LOG_DIR}/peoplepro.test_error.log
        CustomLog ${APACHE_LOG_DIR}/peoplepro.test_access.log combined
    </VirtualHost>
    ```

5. Enable the Virtual Host
    ```
    sudo a2ensite peopleprosaas.conf
    ```

6. Restart Apache
    ```
    sudo service apache2 restart
    ```

7. Clear Config
    ```
    php artisan config:clear
    ```

