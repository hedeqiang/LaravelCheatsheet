# Model
---

### 基础使用 

```php
// 定义一个 Eloquent 模型
class User extends Model {}
// 生成一个 Eloquent 模型
php artisan make:model User
// 指定一个自定义的数据表名称
class User extends Model {
  protected $table = 'my_users';
}
```

### More

```php
Model::create(array('key' => 'value'));
// 通过属性找到第一条相匹配的数据或创造一条新数据
Model::firstOrCreate(array('key' => 'value'));
// 通过属性找到第一条相匹配的数据或实例化一条新数据
Model::firstOrNew(array('key' => 'value'));
// 通过属性找到相匹配的数据并更新，如果不存在即创建
Model::updateOrCreate(array('search_key' => 'search_value'), array('key' => 'value'));
// 使用属性的数组来填充一个模型, 用的时候要小心「Mass Assignment」安全问题 !
Model::fill($attributes);
Model::destroy(1);
Model::all();
Model::find(1);
// 使用双主键进行查找
Model::find(array('first', 'last'));
// 查找失败时抛出异常
Model::findOrFail(1);
// 使用双主键进行查找, 失败时抛出异常
Model::findOrFail(array('first', 'last'));
Model::where('foo', '=', 'bar')->get();
Model::where('foo', '=', 'bar')->first();
Model::where('foo', '=', 'bar')->exists();
// 动态属性查找
Model::whereFoo('bar')->first();
// 查找失败时抛出异常
Model::where('foo', '=', 'bar')->firstOrFail();
Model::where('foo', '=', 'bar')->count();
Model::where('foo', '=', 'bar')->delete();
// 输出原始的查询语句
Model::where('foo', '=', 'bar')->toSql();
Model::whereRaw('foo = bar and cars = 2', array(20))->get();
Model::on('connection-name')->find(1);
Model::with('relation')->get();
Model::all()->take(10);
Model::all()->skip(10);
// 默认的 Eloquent 排序是上升排序
Model::all()->orderBy('column');
Model::all()->orderBy('column','desc');
```

### 软删除 

```php
Model::withTrashed()->where('cars', 2)->get();
// 在查询结果中包括带被软删除的模型
Model::withTrashed()->where('cars', 2)->restore();
Model::where('cars', 2)->forceDelete();
// 查找只带有软删除的模型
Model::onlyTrashed()->where('cars', 2)->get();
```

### 模型关联

```php
// 一对一 - User::phone()
return $this->hasOne('App\Phone', 'foreign_key', 'local_key');
// 一对一 - Phone::user(), 定义相对的关联
return $this->belongsTo('App\User', 'foreign_key', 'other_key');

// 一对多 - Post::comments()
return $this->hasMany('App\Comment', 'foreign_key', 'local_key');
//  一对多 - Comment::post()
return $this->belongsTo('App\Post', 'foreign_key', 'other_key');

// 多对多 - User::roles();
return $this->belongsToMany('App\Role', 'user_roles', 'user_id', 'role_id');
// 多对多 - Role::users();
return $this->belongsToMany('App\User');
// 多对多 - Retrieving Intermediate Table Columns
$role->pivot->created_at;
// 多对多 - 中介表字段
return $this->belongsToMany('App\Role')->withPivot('column1', 'column2');
// 多对多 - 自动维护 created_at 和 updated_at 时间戳
return $this->belongsToMany('App\Role')->withTimestamps();

// 远层一对多 - Country::posts(), 一个 Country 模型可能通过中介的 Users
// 模型关联到多个 Posts 模型(User::country_id)
return $this->hasManyThrough('App\Post', 'App\User', 'country_id', 'user_id');

// 多态关联 - Photo::imageable()
return $this->morphTo();
// 多态关联 - Staff::photos()
return $this->morphMany('App\Photo', 'imageable');
// 多态关联 - Product::photos()
return $this->morphMany('App\Photo', 'imageable');
// 多态关联 - 在 AppServiceProvider 中注册你的「多态对照表」
Relation::morphMap([
    'Post' => App\Post::class,
    'Comment' => App\Comment::class,
]);

// 多态多对多关联 - 涉及数据库表: posts,videos,tags,taggables
// Post::tags()
return $this->morphToMany('App\Tag', 'taggable');
// Video::tags()
return $this->morphToMany('App\Tag', 'taggable');
// Tag::posts()
return $this->morphedByMany('App\Post', 'taggable');
// Tag::videos()
return $this->morphedByMany('App\Video', 'taggable');

// 查找关联
$user->posts()->where('active', 1)->get();
// 获取所有至少有一篇评论的文章...
$posts = App\Post::has('comments')->get();
// 获取所有至少有三篇评论的文章...
$posts = Post::has('comments', '>=', 3)->get();
// 获取所有至少有一篇评论被评分的文章...
$posts = Post::has('comments.votes')->get();
// 获取所有至少有一篇评论相似于 foo% 的文章
$posts = Post::whereHas('comments', function ($query) {
    $query->where('content', 'like', 'foo%');
})->get();

// 预加载
$books = App\Book::with('author')->get();
$books = App\Book::with('author', 'publisher')->get();
$books = App\Book::with('author.contacts')->get();

// 延迟预加载
$books->load('author', 'publisher');

// 写入关联模型
$comment = new App\Comment(['message' => 'A new comment.']);
$post->comments()->save($comment);
// Save 与多对多关联
$post->comments()->saveMany([
    new App\Comment(['message' => 'A new comment.']),
    new App\Comment(['message' => 'Another comment.']),
]);
$post->comments()->create(['message' => 'A new comment.']);

// 更新「从属」关联
$user->account()->associate($account);
$user->save();
$user->account()->dissociate();
$user->save();

// 附加多对多关系
$user->roles()->attach($roleId);
$user->roles()->attach($roleId, ['expires' => $expires]);
// 从用户上移除单一身份...
$user->roles()->detach($roleId);
// 从用户上移除所有身份...
$user->roles()->detach();
$user->roles()->detach([1, 2, 3]);
$user->roles()->attach([1 => ['expires' => $expires], 2, 3]);

// 任何不在给定数组中的 IDs 将会从中介表中被删除。
$user->roles()->sync([1, 2, 3]);
// 你也可以传递中介表上该 IDs 额外的值：
$user->roles()->sync([1 => ['expires' => true], 2, 3]);

```

### 事件

```php
Model::retrieved(function($model){});
Model::creating(function($model){});
Model::created(function($model){});
Model::updating(function($model){});
Model::updated(function($model){});
Model::saving(function($model){});
Model::saved(function($model){});
Model::deleting(function($model){});
Model::deleted(function($model){});
Model::restoring(function($model){});
Model::restored(function($model){});
Model::observe(new FooObserver);
``` 

### Eloquent  配置信息

```php
// 关闭模型插入或更新操作引发的 「mass assignment」异常
Eloquent::unguard();
// 重新开启「mass assignment」异常抛出功能
Eloquent::reguard();
```