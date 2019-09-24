```
return Redirect::to('foo/bar');
return Redirect::to('foo/bar')->with('key', 'value');
return Redirect::to('foo/bar')->withInput(Input::get());
return Redirect::to('foo/bar')->withInput(Input::except('password'));
return Redirect::to('foo/bar')->withErrors($validator);
// 重定向到之前的请求
return Redirect::back();
// 重定向到命名路由（根据命名路由算出 URL）
return Redirect::route('foobar');
return Redirect::route('foobar', array('value'));
return Redirect::route('foobar', array('key' => 'value'));
// 重定向到控制器动作（根据控制器动作算出 URL）
return Redirect::action('FooController@index');
return Redirect::action('FooController@baz', array('value'));
return Redirect::action('FooController@baz', array('key' => 'value'));
// 跳转到目的地址，如果没有设置则使用默认值 foo/bar
return Redirect::intended('foo/bar');
```