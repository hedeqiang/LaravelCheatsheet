```
View::make('path/to/view');
View::make('foo/bar')->with('key', 'value');
View::make('foo/bar')->withKey('value');
View::make('foo/bar', array('key' => 'value'));
View::exists('foo/bar');
// 跨视图共享变量
View::share('key', 'value');
// 视图嵌套
View::make('foo/bar')->nest('name', 'foo/baz', $data);
// 注册一个视图构造器
View::composer('viewname', function($view){});
// 注册多个视图到一个视图构造器中
View::composer(array('view1', 'view2'), function($view){});
// 注册一个视图构造器类
View::composer('viewname', 'FooComposer');
View::creator('viewname', function($view){});
```