```
// 写入文件
Storage::put('avatars/1', $fileContents);
// 指定磁盘
Storage::disk('local')->put('file.txt', 'Contents');
Storage::get('file.jpg');
Storage::exists('file.jpg');
Storage::download('file.jpg',  $name,  $headers);
Storage::url('file.jpg');
Storage::temporaryUrl('file.jpg', now()->addMinutes(5));
Storage::size('file.jpg');
Storage::lastModified('file.jpg');
// 自动为文件名生成唯一的ID...  
Storage::putFile('photos',  new  File('/path/to/photo'));
// 手动指定文件名...  
Storage::putFileAs('photos', new  File('/path/to/photo'), 'photo.jpg');
Storage::prepend('file.log', 'Prepended Text');
Storage::append('file.log', 'Appended Text');
Storage::copy('old/file.jpg', 'new/file.jpg');
Storage::move('old/file.jpg', 'new/file.jpg');
Storage::putFileAs('avatars', $request->file('avatar'), Auth::id());
// 「可见性」是对多个平台的文件权限的抽象
Storage::getVisibility('file.jpg');
Storage::setVisibility('file.jpg',  'public')
Storage::delete('file.jpg');
Storage::delete(['file.jpg',  'file2.jpg']);
// 获取目录下的所有的文件
Storage::files($directory);
Storage::allFiles($directory);
// 获取目录下的所有目录
Storage::directories($directory);
Storage::allDirectories($directory);
// 创建目录
Storage::makeDirectory($directory);
// 删除目录
Storage::deleteDirectory($directory);
```