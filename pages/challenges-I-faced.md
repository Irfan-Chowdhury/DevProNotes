<div align='center'>

# Table of Contents
</div>



- [1. Storage:link not working on hosting cPanel](#1-storagelink-not-working-on-hosting-cpanel)


## 1. Storage:link not working on hosting cPanel

### Problem Statement : 
I've created a storage link with php artisan storage:link and it's working totally fine on localhost, However, when I deploy my project on a shared hosting cPanel, it does not render any images. 

Solutions : 
- Delete the storage link folder created on your local host from your c-panel
-  Create a route to run you php artisan storage:link command as below :

    ```php
    use Illuminate\Support\Facades\Artisan;

    Route::get('/storage_link', function (){ 
        Artisan::call('storage:link'); 
        return 'Success !';
    });
    ```
- On your bowser got to the route /storage_link,.. this will create a new system link to you storage file.

- Your `APP_URL` on `.env` file should be 

    ```bash
    APP_URL=your_site_url
    ```
- Check the `config/filesystems.php`

    ```php
        'public' => [
            'driver' => 'local',
            'root' => storage_path('app/public'),
            'url' => env('APP_URL').'/storage',
            'visibility' => 'public',
        ],
    ```

- Recommended to fetch the image like this - 
    ```php
    isset($path) && (Storage::disk('public')->exists($path)) ? Storage::url($path) : "https://dummyimage.com/50x50/000000/0f6954.png&text=$default";
    ```

