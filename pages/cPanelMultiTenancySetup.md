<div align='center'>

# Multi Tenancy Setup in cPanel
</div>

## General Setup
- Goto your cPanel and upload your app in <b>`public_html`</b>. Remember your project's  files should be exists in root directory I mean "public_html".

## API Setup
- Search or goto  <b>`Manage API Tokens`</b>

- Click on the `Create` button
 ![Manage API Token Page](https://snipboard.io/3sYbCP.jpg)

- Set a API token name and click on `Create` button.
 ![Create API Token](https://snipboard.io/DgLBF1.jpg)

- An API will be created. Copy the API Token and store it. And then click on `Yes, I saved my token` button.
 ![Saved API Token](https://snipboard.io/wReKb9.jpg)

- If you go back `Manage API Token` page, you will see the tokens detail which you created.
![Manage API Token Page](https://snipboard.io/i0IE84.jpg)

- Put the credentials in the `.env` file.
![Manage API Token Page](https://snipboard.io/J3EcUF.jpg)


## Wildcard Sub Domain
You can not create sub-domain through the Multi Tenancy but you can create a `Wild Card Sub Domain`. Follow the instruction - 

- Search and goto `Domains`. And create a new domain by clicking on `Create A New Domain` button.
![Domains Page](https://snipboard.io/ZstM8Q.jpg)

- (i) You have to set a domain name and according to this format : <b>`*.your-domain-name.com`</b> 
<br>
(ii)  And also set "Document Root" name and you have to write <b>`public_html`</b>
<br>
(iii) After completing to do this, then click on `Submit` button.
![Domains Page](https://snipboard.io/WV5rpz.jpg)


- A new domain will be created.
![New Domain Created](https://snipboard.io/vyzCMm.jpg)


<i>Note: You cannot create a wildcard addon domain. You must create a subdomain on an existing domain instead.</i>

## .env
Your value in `.env`  file will be look like this -
![New Domain Created](https://snipboard.io/Oft10q.jpg)


## Replace Code 

- Please goto `Stancl\Tenancy\TenantDatabaseManagers\MySQLDatabaseManager.php`. 
You will see the deafult code of Package.
![Old Code](https://snipboard.io/4edpjv.jpg)


- Now, you have to replace the code given below. Screenshot :
![New Code](https://snipboard.io/YRga4B.jpg)

Code
```
public function createDatabase(TenantWithDatabase $tenant): bool
{
    $database = $tenant->database()->getName();
    $charset = $this->database()->getConfig('charset');
    $collation = $this->database()->getConfig('collation');

    //setting the curl headers
    $headers = array(
        "Authorization: cpanel ".env('CPANEL_USER_NAME').":".env('CPANEL_API_KEY'),
        "Content-Type: text/plain"
    );

    //custom code for creating DB in a cPanel based server
    $url = "https://".env('CENTRAL_DOMAIN').":2083/execute/Mysql/create_database?name=".$database;
    $curl = curl_init($url);
    curl_setopt($curl, CURLOPT_URL, $url);
    curl_setopt($curl, CURLOPT_POST, true);
    curl_setopt($curl, CURLOPT_RETURNTRANSFER, true);
    curl_setopt($curl, CURLOPT_HTTPHEADER, $headers);
    //for debug only!
    curl_setopt($curl, CURLOPT_SSL_VERIFYHOST, false);
    curl_setopt($curl, CURLOPT_SSL_VERIFYPEER, false);
    curl_exec($curl);
    curl_close($curl);

    //custom code for assigning user to DB in a cPanel based server
    $url = "https://".env('CENTRAL_DOMAIN').":2083/execute/Mysql/set_privileges_on_database?user=".env('DB_USERNAME')."&database=".$database."&privileges=ALL";

    $curl = curl_init($url);
    curl_setopt($curl, CURLOPT_URL, $url);
    curl_setopt($curl, CURLOPT_POST, true);
    curl_setopt($curl, CURLOPT_RETURNTRANSFER, true);
    curl_setopt($curl, CURLOPT_HTTPHEADER, $headers);
    //for debug only!
    curl_setopt($curl, CURLOPT_SSL_VERIFYHOST, false);
    curl_setopt($curl, CURLOPT_SSL_VERIFYPEER, false);
    curl_exec($curl);
    curl_close($curl);

    return true;
}
```

#### Done. Run Your App

## Credits
- Helped by [Ashfaqur Rahman](https://github.com/ashfaqdev)
