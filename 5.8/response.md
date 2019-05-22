# Response

---

```php
return Response::make($contents);
return Response::make($contents, 200);
return Response::json(array('key' => 'value'));
return Response::json(array('key' => 'value'))->setCallback(Input::get('callback'));
return Response::download($filepath);
return Response::download($filepath, $filename, $headers);
// 创建一个回应且修改其头部信息的值
$response = Response::make($contents, 200);
$response->header('Content-Type', 'application/json');
return $response;
// 为回应附加上 cookie
return Response::make($content)->withCookie(Cookie::make('key', 'value'));
```