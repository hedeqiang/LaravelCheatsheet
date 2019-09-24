```
Route::get('foo', function(){});
Route::get('foo', 'ControllerName@function');
Route::controller('foo', 'FooController');
```

### 资源路由 

```
Route::resource('posts','PostsController');
// 资源路由器只允许指定动作通过
Route::resource('photo', 'PhotoController',['only' => ['index', 'show']]);
Route::resource('photo', 'PhotoController',['except' => ['update', 'destroy']]);
// 批量注册资源路由
Route::resources(['foo' => 'FooController', 'bar' => 'BarController'])
Route::resources(['foo' => 'FooController', 'bar' => 'BarController'], ['only' => ['index', 'show']])
Route::resources(['foo' => 'FooController', 'bar' => 'BarController'], ['except' => ['update', 'destroy']])
```

### 触发错误 

```
App::abort(404);
$handler->missing(...) in ErrorServiceProvider::boot();
throw new NotFoundHttpException;
```

### 路由参数 

```
Route::get('foo/{bar}', function($bar){});
Route::get('foo/{bar?}', function($bar = 'bar'){});
```

### HTTP 请求方式

```
Route::any('foo', function(){});
Route::post('foo', function(){});
Route::put('foo', function(){});
Route::patch('foo', function(){});
Route::delete('foo', function(){});
// RESTful 资源控制器
Route::resource('foo', 'FooController');
// 为一个路由注册多种请求方式
Route::match(['get', 'post'], '/', function(){});
```

### 安全路由 (TBD)

```
Route::get('foo', array('https', function(){}));
```

### 路由约束

```
Route::get('foo/{bar}', function($bar){})
		->where('bar', '[0-9]+');
Route::get('foo/{bar}/{baz}', function($bar, $baz){})
		->where(array('bar' => '[0-9]+', 'baz' => '[A-Za-z]'))
              
// 设置一个可跨路由使用的模式
 Route::pattern('bar', '[0-9]+')
```  

### HTTP 中间件 

```
// 为路由指定 Middleware
Route::get('admin/profile', ['middleware' => 'auth', function(){}]);
Route::get('admin/profile', function(){})->middleware('auth');
``` 

### 命名路由

```
Route::currentRouteName();
Route::get('foo/bar', array('as' => 'foobar', function(){}));
Route::get('user/profile', [
	'as' => 'profile', 'uses' => 'UserController@showProfile'
]);
Route::get('user/profile', 'UserController@showProfile')->name('profile');
$url = route('profile');
$redirect = redirect()->route('profile');
```

### 路由前缀

```
Route::group(['prefix' => 'admin'], function()
{
	Route::get('users', function(){
		return 'Matches The "/admin/users" URL';
	});
});
```

### 路由命名空间

```
// 此路由组将会传送 'Foo\Bar' 命名空间
Route::group(array('namespace' => 'Foo\Bar'), function(){})
```

### 子域名路由

```
// {sub} 将在闭包中被忽略
Route::group(array('domain' => '{sub}.example.com'), function(){});
```