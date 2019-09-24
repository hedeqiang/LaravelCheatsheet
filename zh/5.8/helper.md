注：数组和字串函数将在 5.9 全面废弃，推荐使用 Arr 和 Str Facade 

### 数组 & 对象

```
// 如果给定的键不存在于该数组，Arr::add 函数将给定的键值对加到数组中
Arr::add(['name' => 'Desk'], 'price', 100); 
// >>> ['name' => 'Desk', 'price' => 100]
// 将数组的每一个数组折成单一数组
Arr::collapse([[1, 2, 3], [4, 5, 6]]);  
// >>> [1, 2, 3, 4, 5, 6]
// 函数返回两个数组，一个包含原本数组的键，另一个包含原本数组的值
Arr::divide(['key1' => 'val1', 'key2' =>'val2'])
// >>> [["key1","key2"],["val1","val2"]]
// 把多维数组扁平化成一维数组，并用「点」式语法表示深度
Arr::dot($array);
// 从数组移除给定的键值对
Arr::except($array, array('key'));
// 返回数组中第一个通过为真测试的元素
Arr::first($array, function($key, $value){}, $default);
// 将多维数组扁平化成一维
 // ['Joe', 'PHP', 'Ruby'];
Arr::flatten(['name' => 'Joe', 'languages' => ['PHP', 'Ruby']]);
// 以「点」式语法从深度嵌套数组移除给定的键值对
Arr::forget($array, 'foo');
Arr::forget($array, 'foo.bar');
// 使用「点」式语法从深度嵌套数组取回给定的值
Arr::get($array, 'foo', 'default');
Arr::get($array, 'foo.bar', 'default');
// 使用「点」式语法检查给定的项目是否存在于数组中
Arr::has($array, 'products.desk');
// 从数组返回给定的键值对
Arr::only($array, array('key'));
// 从数组拉出一列给定的键值对
Arr::pluck($array, 'key');
// 从数组移除并返回给定的键值对
Arr::pull($array, 'key');
// 使用「点」式语法在深度嵌套数组中写入值
Arr::set($array, 'key', 'value');
Arr::set($array, 'key.subkey', 'value');
// 借由给定闭包结果排序数组
Arr::sort($array, function(){});
// 使用 sort 函数递归排序数组
Arr::sortRecursive();
// 使用给定的闭包过滤数组
Arr::where();
// 数组"洗牌"
Arr::shuffle($array,'I-AM-GROOT');
// 数组包裹(如果不是数组，就变成数组，如果是空的，返回[],否则返回原数据）
Arr::wrap($array);
// 返回给定数组的第一个元素
head($array);
// 返回给定数组的最后一个元素
last($array);
```

### 路径

```
// 取得 app 文件夹的完整路径
app_path();
// 取得项目根目录的完整路径
base_path();
// 取得应用配置目录的完整路径
config_path();
// 取得应用数据库目录的完整路径
database_path();
// 取得加上版本号的 Elixir 文件路径
elixir();
// 取得 public 目录的完整路径
public_path();
// 取得 storage 目录的完整路径
storage_path();
```

### 字符串

```
// 将给定的字符串转换成 驼峰式命名
Str::camel($value);
// 返回不包含命名空间的类名称
class_basename($class);
class_basename($object);
// 对给定字符串运行 htmlentities
e('<html>');
// 判断字符串开头是否为给定内容
Str::startsWith('Foo bar.', 'Foo');
// 判断给定字符串结尾是否为指定内容
Str::endsWith('Foo bar.', 'bar.');
// 将给定的字符串转换成 蛇形命名
Str::snake('fooBar');
// 将给定字符串转换成「首字大写命名」: FooBar
Str::studly('foo_bar');
// 根据你的本地化文件翻译给定的语句
trans('foo.bar');
// 根据后缀变化翻译给定的语句
trans_choice('foo.bar', $count);
```

### URLs and Links

```
// 产生给定控制器行为网址
action('FooController@method', $parameters);
// 根据目前请求的协定（HTTP 或 HTTPS）产生资源文件网址
asset('img/photo.jpg', $title, $attributes);
// 根据 HTTPS 产生资源文件网址
secure_asset('img/photo.jpg', $title, $attributes);
// 产生给定路由名称网址
route($route, $parameters, $absolute = true);
// 产生给定路径的完整网址
url('path', $parameters = array(), $secure = null);
```

### 其他

```
// 返回一个认证器实例。你可以使用它取代 Auth facade
auth()->user();
// 产生一个重定向回应让用户回到之前的位置
back();
// 使用 Bcrypt 哈希给定的数值。你可以使用它替代 Hash facade
bcrypt('my-secret-password');
// 从给定的项目产生集合实例
collect(['taylor', 'abigail']);
// 取得设置选项的设置值
config('app.timezone', $default);
// 产生包含 CSRF 令牌内容的 HTML 表单隐藏字段
{!! csrf_field() !!} 
// 5.7+用这个
@csrf
// 取得当前 CSRF 令牌的内容
$token = csrf_token();
// 输出给定变量并结束脚本运行
dd($value);
// var_dump缩写（如果用dump-server,var_dump可能无效）
dump($value);
// 取得环境变量值或返回默认值
$env = env('APP_ENV');
$env = env('APP_ENV', 'production');
// 配送给定事件到所属的侦听器
event(new UserRegistered($user));
// 根据给定类、名称以及总数产生模型工厂建构器
$user = factory(App\User::class)->make();
// 产生拟造 HTTP 表单动作内容的 HTML 表单隐藏字段
{!! method_field('delete') !!}
// 5.7+
@method('delete')
// 取得快闪到 session 的旧有输入数值
$value = old('value');
$value = old('value', 'default');
// 返回重定向器实例以进行 重定向
 return redirect('/home');
// 取得目前的请求实例或输入的项目
$value = request('key', $default = null)
// 创建一个回应实例或获取一个回应工厂实例
return response('Hello World', 200, $headers);
// 可被用于取得或设置单一 session 内容
$value = session('key');
// 在没有传递参数时，将返回 session 实例
$value = session()->get('key');
session()->put('key', $value);
// 返回给定数值
value(function(){ return 'bar'; });
// 取得视图 实例
return view('auth.login');
// 返回给定的数值
$value = with(new Foo)->work();
```