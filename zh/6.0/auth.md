### 用户认证

```php
// 获取 Auth 对象，等同于 Auth Facade
auth();
// 判断当前用户是否已认证（是否已登录）
Auth::check();
// 判断当前用户是否未登录，与 check() 相反
Auth::guest();
// 自定义看守器 默认为 `web`
Auth::guard();
// 获取当前的认证用户
Auth::user();
// 获取当前的认证用户的 ID（未登录情况下会报错）
Auth::id();
// 通过给定的信息来尝试对用户进行认证（成功后会自动启动会话）
Auth::attempt(['email' => $email, 'password' => $password]);
// 通过 Auth::attempt() 传入 true 值来开启 '记住我' 功能
Auth::attempt($credentials, true);
// 注册尝试登录的事件监听器
Auth::attempting($callback);
// 只针对一次的请求来认证用户
Auth::once($credentials);
// 使用 ID 登录，无 Cookie 和会话登录
Auth::onceUsingId($id);
// 登录一个指定用户到应用上
Auth::login(User::find(1), $remember = false);
// 检测是否记住了登录
Auth::viaRemember();
// 登录指定用户 ID 的用户到应用上
Auth::loginUsingId(1, $remember = false);
// 使用户退出登录（清除会话）
Auth::logout();
// 清除当前用户的其他会话
Auth::logoutOtherDevices('password', $attribute = 'password');
// 验证用户凭证
Auth::validate($credentials);
// 使用 HTTP 的基本认证方式来认证
Auth::basic('username');
// 执行「HTTP Basic」登录尝试，只认证一次
Auth::onceBasic();
// 发送密码重置提示给用户
Password::remind($credentials, function($message, $user){});
```

### 用户授权

```
// 定义权限
Gate::define('update-post', 'Class@method');
Gate::define('update-post', function ($user, $post) {...});
// 传递多个参数
Gate::define('delete-comment', function ($user, $post, $comment) {});
// 一次性的定义多个 Gate 方法
Gate::resource('posts',  'App\Policies\PostPolicy');
// 检测权限是否被定义
Gate::has('update-post');

// 检查权限
Gate::denies('update-post', $post);
Gate::allows('update-post', $post);
Gate::check('update-post', $post);
// 指定用户进行检查
Gate::forUser($user)->allows('update-post', $post);
// 在 User 模型下，使用 Authorizable trait
User::find(1)->can('update-post', $post);
User::find(1)->cannot('update-post', $post);
User::find(1)->cant('update-post', $post);

// 拦截所有检查，返回 bool
Gate::before(function ($user, $ability) {});
// 设置每一次验证的回调
Gate::after(function ($user, $ability, $result, $arguments) {});

// Blade 模板语法
@can('update-post', $post)
@endcan
// 支持 else 表达式
@can('update-post', $post)
@else
@endcan
// 无权限判断
@cannot
@endcannot

// 生成一个新的策略
php artisan make:policy PostPolicy
php artisan make:policy PostPolicy --model=Post
// `policy` 帮助函数
policy($post)->update($user, $post)

// 控制器授权
$this->authorize('update', $post);
// 指定用户 $user 授权
$this->authorizeForUser($user, 'update', $post);
// 控制器的 __construct 中授权资源控制器
$this->authorizeResource(Post::class,  'post');

// AuthServiceProvider->boot() 里修改策略自动发现的逻辑
Gate::guessPolicyNamesUsing(function ($modelClass) {
	// 返回模型对应的策略名称，如：// 'App\Model\User' => 'App\Policies\UserPolicy',
	return 'App\Policies\\'.class_basename($modelClass).'Policy';
});

// 中间件指定模型实例
Route::put('/post/{post}',  function  (Post $post)  { ... })->middleware('can:update,post');
// 中间件未指定模型实例
Route::post('/post',  function  ()  { ... })->middleware('can:create,App\Post');
```