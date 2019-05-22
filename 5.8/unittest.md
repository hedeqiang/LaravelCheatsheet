# UnitTest

---

### 安装和运行

```php
// 将其加入到 composer.json 并更新:
composer require "phpunit/phpunit:4.0.*"
// 运行测试 (在项目根目录下运行)
./vendor/bin/phpunit
```

### 断言

```php
$this->assertTrue(true);
$this->assertEquals('foo', $bar);
$this->assertCount(1,$times);
$this->assertResponseOk();
$this->assertResponseStatus(403);
$this->assertRedirectedTo('foo');
$this->assertRedirectedToRoute('route.name');
$this->assertRedirectedToAction('Controller@method');
$this->assertViewHas('name');
$this->assertViewHas('age', $value);
$this->assertSessionHasErrors();
// 由单个 key 值来假定 session 有错误...
$this->assertSessionHasErrors('name');
// 由多个 key 值来假定 session 有错误...
$this->assertSessionHasErrors(array('name', 'age'));
$this->assertHasOldInput();
```

### 访问路由

```php
$response = $this->call($method, $uri, $parameters, $files, $server, $content);
$response = $this->callSecure('GET', 'foo/bar');
$this->session(['foo' => 'bar']);
$this->flushSession();
$this->seed();
$this->seed($connection);
```