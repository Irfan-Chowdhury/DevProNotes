<div align='center'>

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
        ServerName your_site_name.test
        ServerAlias www.your_site_name.test
            
        DocumentRoot /path/to/your/laravel/project/public

        <Directory /path/to/your/laravel/project/public>
            Options Indexes FollowSymLinks
            AllowOverride All
            Require all granted
        </Directory>

        ErrorLog ${APACHE_LOG_DIR}/your_file_name.test_error.log
        CustomLog ${APACHE_LOG_DIR}/your_file_name.test_access.log combined
    </VirtualHost>
    ```
    
    For an example - 

    if your file name is "peopleprosaas.conf"

    ```bash
	<VirtualHost *:80>
	    ServerName  peoplepro-hrm-crm.test
	    ServerAlias www.peoplepro-hrm-crm.test

	    DocumentRoot /var/www/html/peoplepro/peoplepro-hrm-crm/public

	    <Directory /var/www/html/peoplepro/peoplepro-hrm-crm/public>
		Options Indexes FollowSymLinks
		AllowOverride All
		Require all granted
	    </Directory>

	    ErrorLog ${APACHE_LOG_DIR}/peopleprosaas-error.log
	    CustomLog ${APACHE_LOG_DIR}/peopleprosaas-access.log combined
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

8. After setup don't forget to write the central domain in `.env` in your application
    ```
    CENTRAL_DOMAIN=peopleprosaas.test
    ```

## Return Back Default

1. Remove the Custom Domain from the Hosts File
    ```
    sudo nano /etc/hosts
    ```

2. Disable the Virtual Host (Apache)
    ```
    sudo a2dissite peopleprosaas.conf
    ```

3. Restart Apache
    ```
    sudo service apache2 restart
    ```

4. Clear Laravel Configuration Cache (Optional)
    ```
    php artisan config:clear
    ```

## Rename the Configuration File

1. Run this command
    ```
    sudo mv /etc/apache2/sites-available/peoplepro.test.conf /etc/apache2/sites-available/newname.conf
    ```

2. Update the Virtual Host Configuration
    ```
    sudo nano /etc/apache2/sites-available/newname.conf
    ```

3. Enable the Updated Virtual Host
    ```
    sudo a2ensite newname.conf
    ```

4. Restart Apache
    ```
    sudo service apache2 restart
    ```
