# Lang

---

```php
App::setLocale('en');
Lang::get('messages.welcome');
Lang::get('messages.welcome', array('foo' => 'Bar'));
Lang::has('messages.welcome');
Lang::choice('messages.apples', 10);
// Lang::get 的别名
trans('messages.welcome');
// Lang::choice 的别名
trans_choice('messages.apples',  10)
// 辅助函数
__('messages.welcome')
```