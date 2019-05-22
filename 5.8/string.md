# String

---

```php
// 将 UTF-8 的值直译为 ASCII 类型的值
Str::ascii($value)
Str::camel($value)
Str::contains($haystack, $needle)
Str::endsWith($haystack, $needles)
Str::finish($value, $cap)
Str::is($pattern, $value)
Str::length($value)
Str::limit($value, $limit = 100, $end = '...')
Str::lower($value)
Str::words($value, $words = 100, $end = '...')
Str::plural($value, $count = 2)
// 生成更加真实的 "随机" 字母数字字符串.
Str::random($length = 16)
// 生成一个 "随机" 字母数字字符串.
Str::quickRandom($length = 16)
Str::upper($value)
Str::title($value)
Str::singular($value)
Str::slug($title, $separator = '-')
Str::snake($value, $delimiter = '_')
Str::startsWith($haystack, $needles)
Str::studly($value)
Str::macro($name, $macro)
```