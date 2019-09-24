```
composer create-project laravel/laravel folder_name
composer create-project laravel/laravel folder_name --prefer-dist "5.8.*"
composer install
composer install --prefer-dist
composer update
composer update package/name
composer dump-autoload [--optimize]
composer self-update
composer require [options] [--] [vendor/packages]...
// 全局安装
composer require global vendor/packages
// 罗列所有扩展包括版本信息
composer show
```