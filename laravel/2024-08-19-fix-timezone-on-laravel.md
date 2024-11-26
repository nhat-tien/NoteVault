## Issue
- Laravel save timestamp in database with wrong timezone
- Laravel return resource json with wrong timestamp

## Solution

**In Laravel version 10**

Follow below steps:

### 1. Replace `UTC` by your timezone in `config/app.php`

*Example*
```php
<?php
return [
    /*
    |--------------------------------------------------------------------------
    | Application Timezone
    |--------------------------------------------------------------------------
    |
    | Here you may specify the default timezone for your application, which
    | will be used by the PHP date and date-time functions. We have gone
    | ahead and set this to a sensible default for you out of the box.
    |
    */
    // Before
    // 'timezone' => 'UTC',
    // After
    'timezone' => 'Asia/Ho_Chi_Minh',
]
```

### 2. Try to refresh your config cache

```bash
php artisan config:clear
php artisan config:cache
```

if you can not delete config cache, try using `rm` command remove `bootstrap/cache/config.php`,  `bootstrap/cache/packages.php`, `bootstrap/cache/services.php`.

### 3. Add method to your models which use time, datetime

```php
<?php
use DateTimeInterface; // <--- remember add this line

class YourModel extends Model {

    // ---- code ----

    public function serializeDate(DateTimeInterface $date): string
    {
        return $date->format('Y-m-d H:i:s'); // <- you can modify this template
    }

}
```

Now in Resource, you use that method:

```php
<?php

    public function toArray(Request $request): array
    {
        return [
            // ---- code... ------
            'createdAt' => $this->serializeDate($this->created_at),
            'updatedAt' => $this->serializeDate($this->updated_at),
        ];
    }
```

### 4. Done, test your API again


