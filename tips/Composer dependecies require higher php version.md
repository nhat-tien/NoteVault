---
tags:
  - php
  - laravel
date: "2024-03-22"
---


1. Xóa vendor, composer.lock
2. Chỉnh sửa php trong `composer.json` thành version của host

```json
"require": {
        "php": "7.4",
},
"config": {
        "platform": {
            "php": "7.4"
        },
		    "platform-check": false,
}
```

3. Chạy `composer install` để tải lại vendor
 
```shell
composer install
```
