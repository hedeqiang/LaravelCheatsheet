# Event

---

```php
// 1. EventServiceProvider 类里的 $listen 属性
protected $listen =['App\Events\OrderShipped' => ['App\Listeners\SendShipmentNotification']];
// 2. 生成监听类
php artisan event:generate

// 触发命令
Event::fire($event, $payload = [], $halt = false);
Event::dispatch($event, $payload = [], $halt = false);
event($event, $payload = [], $halt = false);
// 触发命令并等待
Event::until($event, $payload = []);
// 注册一个事件监听器.
// void listen(string|array $events, mixed $listener, int $priority)
Event::listen('App\Events\UserSignup', function($bar){});
Event::listen('event.*', function($bar){}); // 通配符监听器
Event::listen('foo.bar', 'FooHandler', 10);
Event::listen('foo.bar', 'BarHandler', 5);
// 你可以直接在处理逻辑中返回 false 来停止一个事件的传播.
Event::listen('foor.bar', function($event){ return false; });
Event::subscribe('UserEventHandler');
// 获取所有监听者
Event::getListeners($eventName);
// 移除事件及其对应的监听者
Event::forget($event);
// 将事件推入堆栈中等待执行
Event::push($event, $payload = []);
// 移除指定的堆栈事件
Event::flush($event);
// 移除所有堆栈中的事件
Event::forgetPushed();
```