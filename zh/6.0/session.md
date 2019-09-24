```
Session::get('key');
// 从会话中读取一个条目
 Session::get('key', 'default');
Session::get('key', function(){ return 'default'; });
// 获取 session 的 ID
Session::getId();
// 增加一个会话键值数据
Session::put('key', 'value');
// 将一个值加入到 session 的数组中
Session::push('foo.bar','value');
// 返回 session 的所有条目
Session::all();
// 检查 session 里是否有此条目
Session::has('key');
// 从 session 中移除一个条目
Session::forget('key');
// 从 session 中移除所有条目
Session::flush();
// 生成一个新的 session 标识符
Session::regenerate();
// 把一条数据暂存到 session 中
Session::flash('key', 'value');
// 清空所有的暂存数据
Session::reflash();
// 重新暂存当前暂存数据的子集
Session::keep(array('key1', 'key2'));
```