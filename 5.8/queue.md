# Queue

---

```php
Queue::push('SendMail', array('message' => $message));
Queue::push('SendEmail@send', array('message' => $message));
Queue::push(function($job) use $id {});
// 在多个 workers 中使用相同的负载
Queue::bulk(array('SendEmail', 'NotifyUser'), $payload);
// 开启队列监听器
php artisan queue:listen
php artisan queue:listen connection
php artisan queue:listen --timeout=60
// 只处理第一个队列任务
php artisan queue:work
// 在后台模式启动一个队列 worker
php artisan queue:work --daemon
// 为失败的任务创建 migration 文件
php artisan queue:failed-table
// 监听失败任务
php artisan queue:failed
// 通过 id 删除失败的任务
php artisan queue:forget 5
// 删除所有失败任务
php artisan queue:flush
// 因为队列不会默认使用 PHP memory 参数，需要在队列指定(单位默认mb)
php artisan queue:work --memory=50
```