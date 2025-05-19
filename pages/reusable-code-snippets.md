<div align='center'>

# Table of Contents
</div>

- [1. Use SweetAlert2](#1-use-sweetalert2)


## 1. Use SweetAlert2 

In Laravel Blade file, just add following code

- Add `script` inside the `head` tag

```php
<head>
    ....
    <script src="https://cdn.jsdelivr.net/npm/sweetalert2@11"><script>
</head>
```

- If you want use laravel session message, add these following code before `</body>` close : 

```php
<body>
....

@if(session('success'))
<script>
    Swal.fire({
        icon: 'success',
        title: 'Success!',
        text: '{{ session('success') }}',
        confirmButtonColor: '#3085d6',
        timer: 3000
    });
</script>
@endif

@if($errors->any())
<script>
    Swal.fire({
        icon: 'error',
        title: 'Validation Errors',
        html: `{!! implode('<br>', $errors->all()) !!}`,
        confirmButtonColor: '#d33',
    });
</script>
@endif

</body>
```

- In Controller please following this code - 

```php

    $request->validate([
        //Validation conditions logic
    ]);

    try {
        //Other codes
        return redirect()->back()->with('success', 'Data created successfully');

    } catch (Exception $e) {

        return back()->withErrors([$e->getMessage()]);

    }
```
It will display validation message and custom messages both.
