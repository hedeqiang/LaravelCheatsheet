# Artisan

---

```php
// 针对命令显示帮助信息
php artisan --help OR -h
// 抑制输出信息
php artisan --quiet OR -q
// 打印 Laravel 的版本信息
php artisan --version OR -V
// 不询问任何交互性的问题
php artisan --no-interaction OR -n
// 强制输出 ANSI 格式
php artisan --ansi
// 禁止输出 ANSI 格式
php artisan --no-ansi
// 显示当前命令行运行的环境
php artisan --env
// -v|vv|vvv 通过增加 v 的个数来控制命令行输出内容的详尽情况: 1 个代表正常输出, 2 个代表输出更多消息, 3 个代表调试
php artisan --verbose
// 移除编译优化过的文件 (storage/frameworks/compiled.php)
php artisan clear-compiled
// 显示当前框架运行的环境
php artisan env
// 显示某个命令的帮助信息
php artisan help
// 显示所有可用的命令
php artisan list
// 进入应用交互模式
php artisan tinker
// 配合 dump() 函数调试数据
php artisan dump-server
// 进入维护模式
php artisan down
// 退出维护模式
php artisan up
// 优化框架性能
// --force    强制编译已写入文件 (storage/frameworks/compiled.php)
// --psr      不对 Composer 的 dump-autoload 进行优化
php artisan optimize [--force] [--psr]
// 更改前端预设
// type_name (可以是 none, bootstrap, vue, react)
php artisan preset [options] [--] type_name
// 启动内置服务器
php artisan serve
// 更改默认端口
php artisan serve --port 8080
// 使其在本地服务器外也可正常工作
php artisan serve --host 0.0.0.0
// 更改应用命名空间
php artisan app:name namespace
// 清除过期的密码重置令牌
php artisan auth:clear-resets

// 清空应用缓存
php artisan cache:clear
// 移除 key_name 对应的缓存
php artisan cache:forget key_name [<store>]
// 创建缓存数据库表 migration
php artisan cache:table

// 合并所有的配置信息为一个，提高加载速度
php artisan config:cache
// 移除配置缓存文件
php artisan config:clear

// 程序内部调用 Artisan 命令
$exitCode = Artisan::call('config:cache');
// 运行所有的 seed 假数据生成类
// --class      可以指定运行的类，默认是: "DatabaseSeeder"
// --database   可以指定数据库
// --force      当处于生产环境时强制执行操作
php artisan db:seed [--class[="..."]] [--database[="..."]] [--force]

// 基于注册的信息，生成遗漏的 events 和 handlers
php artisan event:generate
// 罗列所有事件和监听器
php artisan event:list
// 缓存事件和监听器
php artisan event:cache
// 清除事件和监听器缓存
php artisan event:clear

// 生成新的处理器类
// --command      需要处理器处理的命令类名字
php artisan handler:command [--command="..."] name
// 创建一个新的时间处理器类
// --event        需要处理器处理的事件类名字
// --queued       需要处理器使用队列话处理的事件类名字
php artisan handler:event [--event="..."] [--queued] name

// 生成应用的 key（会覆盖）
php artisan key:generate

// 发布本地化翻译文件到 resources 文件下
// locales: 逗号分隔，如 zh_CN,tk,th [默认是: "all"]
php artisan lang:publish [options] [--] [<locales>]

// 创建用户认证脚手架
php artisan make:auth
// 创建 Channel 类
php artisan make:channel name
// 在默认情况下, 这将创建未加入队列的自处理命令
// 通过 --handler 标识来生成一个处理器, 用 --queued 来使其入队列.
php artisan make:command [--handler] [--queued] name
// 创建一个新的 Artisan 命令
//  --command     命令被调用的名称。 (默认为: "command:name")
php artisan make:console [--command[="..."]] name
// 创建一个新的资源控制器
// --plain      生成一个空白的控制器类
php artisan make:controller [--plain] name
php artisan make:controller App\\Admin\\Http\\Controllers\\DashboardController
// 创建一个新的事件类
php artisan make:event name
// 创建异常类
php artisan make:exception name
// 创建模型工厂类
php artisan make:factory name
// 创建一个队列任务文件
php artisan make:job 
// 创建一个监听者类
php artisan make:listener name
// 创建一个新的邮件类
php artisan make:mail name
// 创建一个新的中间件类
php artisan make:middleware name
// 创建一个新的迁移文件
// --create     将被创建的数据表.
// --table      将被迁移的数据表.
php artisan make:migration [--create[="..."]] [--table[="..."]] name
// 创建一个新的 Eloquent 模型类
php artisan make:model User
php artisan make:model Models/User
// 新建一个消息通知类
php artisan make:notification TopicRepliedNotification
// 新建一个模型观察者类
php artisan make:observer UserObserver
// 创建授权策略
php artisan make:policy PostPolicy
// 创建一个新的服务提供者类
php artisan make:provider name
// 创建一个新的表单请求类
php artisan make:request name
// 创建一个 API 资源类
php artisan make:resource name
// 新建验证规则类
php artisan make:rule name
// 创建模型脚手架
// <name> 模型名称，如 Post
// -s, --schema=SCHEMA 表结构如：--schema="title:string"
// -a, --validator[=VALIDATOR] 表单验证，如：--validator="title:required"
// -l, --localization[=LOCALIZATION] 设置本地化信息，如：--localization="key:value"
// -b, --lang[=LANG] 设置本地化语言 --lang="en"
// -f, --form[=FORM] 使用 Illumintate/Html Form 来生成表单选项，默认为 false
// -p, --prefix[=PREFIX] 表结构前缀，默认 false
php artisan make:scaffold  [options] [--] <name>
// 生成数据填充类
php artisan make:seeder
// 生成测试类
php artisan make:test

// 数据库迁移
// --database   指定数据库连接（下同）
// --force      当处于生产环境时强制执行，不询问（下同）
// --path       指定单独迁移文件地址
// --pretend    把将要运行的 SQL 语句打印出来（下同）
// --seed       Seed 任务是否需要被重新运行（下同）
php artisan migrate [--database[="..."]] [--force] [--path[="..."]] [--pretend] [--seed]
// 创建迁移数据库表
php artisan migrate:install [--database[="..."]]
// Drop 所有数据表并重新运行 Migration
php artisan migrate:fresh
// 重置并重新运行所有的 migrations
// --seeder     指定主 Seeder 的类名
php artisan migrate:refresh [--database[="..."]] [--force] [--seed] [--seeder[="..."]]
// 回滚所有的数据库迁移
php artisan migrate:reset [--database[="..."]] [--force] [--pretend]
// 回滚最最近一次运行的迁移任务
php artisan migrate:rollback [--database[="..."]] [--force] [--pretend]
// migrations 数据库表信息
php artisan migrate:status

// 为数据库消息通知创建一个表迁移类
php artisan notifications:table
// 清除缓存的 bootstrap 文件
php artisan optimize:clear
// 扩展包自动发现
php artisan package:discover

// 为队列数据库表创建一个新的迁移
php artisan queue:table
// 监听指定的队列
// --queue      被监听的队列
// --delay      给执行失败的任务设置延时时间 (默认为零: 0)
// --memory     内存限制大小，单位为 MB (默认为: 128)
// --timeout    指定任务运行超时秒数 (默认为: 60)
// --sleep      等待检查队列任务的秒数 (默认为: 3)
// --tries      任务记录失败重试次数 (默认为: 0)
php artisan queue:listen [--queue[="..."]] [--delay[="..."]] [--memory[="..."]] [--timeout[="..."]] [--sleep[="..."]] [--tries[="..."]] [connection]
// 查看所有执行失败的队列任务
php artisan queue:failed
// 为执行失败的数据表任务创建一个迁移
php artisan queue:failed-table
// 清除所有执行失败的队列任务
php artisan queue:flush
// 删除一个执行失败的队列任务
php artisan queue:forget
// 在当前的队列任务执行完毕后, 重启队列的守护进程
php artisan queue:restart
// 对指定 id 的执行失败的队列任务进行重试(id: 失败队列任务的 ID)
php artisan queue:retry id
// 指定订阅 Iron.io 队列的链接
// queue: Iron.io 的队列名称.
// url: 将被订阅的 URL.
// --type       指定队列的推送类型.
php artisan queue:subscribe [--type[="..."]] queue url
// 处理下一个队列任务
// --queue      被监听的队列
// --daemon     在后台模式运行
// --delay      给执行失败的任务设置延时时间 (默认为零: 0)
// --force      强制在「维护模式下」运行
// --memory     内存限制大小，单位为 MB (默认为: 128)
// --sleep      当没有任务处于有效状态时, 设置其进入休眠的秒数 (默认为: 3)
// --tries      任务记录失败重试次数 (默认为: 0)
php artisan queue:work [--queue[="..."]] [--daemon] [--delay[="..."]] [--force] [--memory[="..."]] [--sleep[="..."]] [--tries[="..."]] [connection]

// 生成路由缓存文件来提升路由效率
php artisan route:cache
// 移除路由缓存文件
php artisan route:clear
// 显示已注册过的路由
php artisan route:list

// 运行计划命令
php artisan schedule:run

// 为 session 数据表生成迁移文件
php artisan session:table
// 创建 "public/storage" 到 "storage/app/public" 的软链接
php artisan storage:link

// 从 vendor 的扩展包中发布任何可发布的资源
// --force        重写所有已存在的文件
// --provider     指定你想要发布资源文件的服务提供者
// --tag          指定你想要发布标记资源.
php artisan vendor:publish [--force] [--provider[="..."]] [--tag[="..."]]
php artisan tail [--path[="..."]] [--lines[="..."]] [connection]

// 缓存视图文件以提高效率
php artisan view:cache
// 清除视图文件缓存
php artisan view:clear
```