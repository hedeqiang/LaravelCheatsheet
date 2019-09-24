```
Input::get('key');
// 指定默认值
Input::get('key', 'default');
Input::has('key');
Input::all();
// 只取回 'foo' 和 'bar'，返回数组
Input::only('foo', 'bar');
// 取除了 'foo' 的所有用户输入数组
Input::except('foo');
Input::flush();
// 字段 'key' 是否有值，返回 boolean
Input::filled('key');
```

### 会话周期内 Input

```
// 清除会话周期内的输入
Input::flash();
// 清除会话周期内的指定输入
Input::flashOnly('foo', 'bar');
// 清除会话周期内的除了指定的其他输入
Input::flashExcept('foo', 'baz');
// 取回一个旧的输入条目
Input::old('key','default_value');
```

### Files

```
// 使用一个已上传的文件
Input::file('filename');
// 判断文件是否已上传
Input::hasFile('filename');
// 获取文件属性
Input::file('name')->getRealPath();
Input::file('name')->getClientOriginalName();
Input::file('name')->getClientOriginalExtension();
Input::file('name')->getSize();
Input::file('name')->getMimeType();
// 移动一个已上传的文件
Input::file('name')->move($destinationPath);
// 移动一个已上传的文件，并设置新的名字
Input::file('name')->move($destinationPath, $fileName);
```