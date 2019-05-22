# Request

---

```php
//获取请求参数 form-data 与 raw 请求类型
request()->input();
// url: http://xx.com/aa/bb
Request::url();
// 路径: /aa/bb
Request::path();
// 获取请求 Uri: /aa/bb/?c=d
Request::getRequestUri();
// 返回用户的 IP
Request::ip();
// 获取 Uri: http://xx.com/aa/bb/?c=d
Request::getUri();
// 获取查询字符串: c=d
Request::getQueryString();
// 获取请求端口 (例如 80, 443 等等)
Request::getPort();
// 判断当前请求的 URI 是否可被匹配
Request::is('foo/*');
// 获取 URI 的分段值 (索引从 1 开始)
Request::segment(1);
// 从请求中取回头部信息
Request::header('Content-Type');
// 从请求中取回服务器变量
Request::server('PATH_INFO');
// 判断请求是否是 AJAX 请求
Request::ajax();
// 判断请求是否使用 HTTPS
Request::secure();
// 获取请求方法
Request::method();
// 判断请求方法是否是指定类型的
Request::isMethod('post');
// 获取原始的 POST 数据
Request::instance()->getContent();
// 获取请求要求返回的格式
Request::format();
// 判断 HTTP Content-Type 头部信息是否包含 */json
Request::isJson();
// 判断 HTTP Accept 头部信息是否为 application/json
Request::wantsJson();
```