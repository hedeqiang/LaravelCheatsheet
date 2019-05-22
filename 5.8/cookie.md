# Cookie

---

```php
// 等于 Cookie
cookie();
request()->cookie('name');
Cookie::get('key');
Cookie::get('key', 'default');
// 创建一个永久有效的 cookie
Cookie::forever('key', 'value');
// 创建一个 N 分钟有效的 cookie
Cookie::make('key', 'value', 'minutes');
cookie('key', 'value', 'minutes');
// 在回应之前先积累 cookie，回应时统一返回
Cookie::queue('key', 'value', 'minutes');
// 移除 Cookie
Cookie::forget('key');
// 从 response 发送一个 cookie
$response = Response::make('Hello World');
$response->withCookie(Cookie::make('name', 'value', $minutes));
// 设置未加密 Cookie app/Http/Middleware/EncryptCookies.php
EncryptCookies->except = ['cookie_name_1'];
```