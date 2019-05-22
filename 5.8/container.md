# Container

---

```php
App::bind('foo', function($app){ return new Foo; });
App::make('foo');
// 如果存在此类, 则返回
App::make('FooBar');
// 单例模式实例到服务容器中
App::singleton('foo', function(){ return new Foo; });
// 将已实例化的对象注册到服务容器中
App::instance('foo', new Foo);
// 注册绑定规则到服务容器中
App::bind('FooRepositoryInterface', 'BarRepository');
// 绑定基本值
App::when('App\Http\Controllers\UserController')->needs('$variableName')->give($value);
// 标记
$this->app->tag(['SpeedReport',  'MemoryReport'],  'reports');
// 给应用注册一个服务提供者
App::register('FooServiceProvider');
// 监听容器对某个对象的解析
App::resolving(function($object){});
resolve('HelpSpot\API');
```