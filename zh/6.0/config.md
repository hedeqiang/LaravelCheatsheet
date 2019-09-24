```
// config/app.php 里的 timezone 配置项
Config::get('app.timezone')
Config::get('app.timezone', 'default');
Config::set('database.default', 'sqlite');
// config() 等同于 Config Facade
config()->get('app.timezone');
config('app.timezone', 'default');   // get
config(['database.default' => 'sqlite']); // set
```