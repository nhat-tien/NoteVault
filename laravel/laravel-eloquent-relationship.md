```php
//class User
return $this->hasOne(Phone::class, 'foreign_key', 'local_key');
```

`foreign_key`: của bảng Phone, (Mặc đinh là `user_id`)
`local_key`: của bảng User, (Mặc định là `id`)


```php
// class Phone
/**
 * Get the user that owns the phone.
 */
public function user(): BelongsTo
{
    return $this->belongsTo(User::class, 'foreign_key', 'owner_key');
}
```

`foreign_key`: của bảng Phone, (Mặc đinh là `user_id`)
`owner_key`: của bảng User, (Mặc định là `id`)