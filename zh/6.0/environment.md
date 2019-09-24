```
$environment = app()->environment();
$environment = App::environment();
// 判断当环境是否为 local
if (app()->environment('local')){}
// 判断当环境是否为 local 或 staging...
if (app()->environment(['local', 'staging'])){}
```