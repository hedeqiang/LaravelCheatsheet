# SSH

---

### Executing Commands

```php
SSH::run(array $commands);
// 指定 remote, 否则将使用默认值
SSH::into($remote)->run(array $commands);
SSH::run(array $commands, function($line)
{
  echo $line.PHP_EOL;
});
```

### 任务

```php
// 定义任务
SSH::define($taskName, array $commands);
// 执行任务
SSH::task($taskName, function($line)
{
  echo $line.PHP_EOL;
});
```

### SFTP 上传

```php
SSH::put($localFile, $remotePath);
SSH::putString($string, $remotePath);
```