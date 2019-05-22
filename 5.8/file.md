# File

---

```php
File::exists($path);
File::get($path, $lock = false);
// 加锁读取文件内容
File::sharedGet($path);
// 获取文件内容，不存在会抛出 FileNotFoundException 异常
File::getRequire($path);
// 获取文件内容, 仅能引入一次
File::requireOnce($file);
// 生成文件路径的 MD5 哈希
File::hash($path);
// 将内容写入文件
File::put($path, $contents, $lock = false);
// 写入文件，存在的话覆盖写入
File::replace($path, $content);
// 将内容添加在文件原内容前面
File::prepend($path, $data);
// 将内容添加在文件原内容后
File::append($path, $data);
// 修改路径权限
File::chmod($path, $mode = null);
// 通过给定的路径来删除文件
File::delete($paths);
// 将文件移动到新目录下
File::move($path, $target);
// 将文件复制到新目录下
File::copy($path, $target);
// 创建硬连接
File::link($target, $link);
// 从文件路径中提取文件名，不包含后缀
File::name($path);
// 从文件路径中提取文件名，包含后缀
File::basename($path);
// 获取文件路径名称
File::dirname($path);
// 从文件的路径地址提取文件的扩展
File::extension($path);
// 获取文件类型
File::type($path);
// 获取文件 MIME 类型
File::mimeType($path);
// 获取文件大小
File::size($path);
// 获取文件的最后修改时间
File::lastModified($path);
// 判断给定的路径是否是文件目录
File::isDirectory($directory);
// 判断给定的路径是否是可读取
File::isReadable($path);
// 判断给定的路径是否是可写入的
File::isWritable($path);
// 判断给定的路径是否是文件
File::isFile($file);
// 查找能被匹配到的路径名
File::glob($pattern, $flags = 0);
// 获取一个目录下的所有文件, 以数组类型返回
File::files($directory, $hidden = false);
// 获取一个目录下的所有文件 (递归).
File::allFiles($directory, $hidden = false);
// 获取一个目录内的目录
File::directories($directory);
// 创建一个目录
File::makeDirectory($path, $mode = 0755, $recursive = false, $force = false);
// 移动目录
File::moveDirectory($from, $to, $overwrite = false);
// 将文件夹从一个目录复制到另一个目录下
File::copyDirectory($directory, $destination, $options = null);
// 删除目录
File::deleteDirectory($directory, $preserve = false);
// 递归式删除目录
File::deleteDirectories($directory);
// 清空指定目录的所有文件和文件夹
File::cleanDirectory($directory);
```