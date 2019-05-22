# Log

---

```PHP
// 记录器提供了 7 种在 RFC 5424 标准内定义的记录等级:
// debug, info, notice, warning, error, critical, and alert.
Log::info('info');
Log::info('info',array('context'=>'additional info'));
Log::error('error');
Log::warning('warning');
// 获取 monolog 实例
Log::getMonolog();
// 添加监听器
Log::listen(function($level, $message, $context) {});
```

### 记录 SQL 查询语句 

```php
// 开启 log
DB::connection()->enableQueryLog();
// 获取已执行的查询数组
DB::getQueryLog();
```