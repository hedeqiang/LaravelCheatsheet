### 基本使用

```
DB::connection('connection_name');
// 运行数据库查询语句
$results = DB::select('select * from users where id = ?', [1]);
$results = DB::select('select * from users where id = :id', ['id' => 1]);
// 运行普通语句
DB::statement('drop table users');
// 监听查询事件
DB::listen(function($sql, $bindings, $time) { code_here; });
// 数据库事务处理
DB::transaction(function() {
	DB::table('users')->update(['votes' => 1]);
	DB::table('posts')->delete();
});
DB::beginTransaction();
DB::rollBack();
DB::commit();

// 获取表前缀
DB::getTablePrefix()
```

### 查询语句构造器 

```
// 取得数据表的所有行
DB::table('name')->get();
// 取数据表的部分数据
DB::table('users')->chunk(100, function($users) {
  foreach ($users as $user) {
      //
  }
});
// 取回数据表的第一条数据
$user = DB::table('users')->where('name', 'John')->first();
DB::table('name')->first();
// 从单行中取出单列数据
$name = DB::table('users')->where('name', 'John')->pluck('name');
DB::table('name')->pluck('column');
// 取多行数据的「列数据」数组
$roles = DB::table('roles')->lists('title');
$roles = DB::table('roles')->lists('title', 'name');
// 指定一个选择字段
$users = DB::table('users')->select('name', 'email')->get();
$users = DB::table('users')->distinct()->get();
$users = DB::table('users')->select('name as user_name')->get();
// 添加一个选择字段到一个已存在的查询语句中
$query = DB::table('users')->select('name');
$users = $query->addSelect('age')->get();
// 使用 Where 运算符
$users = DB::table('users')->where('votes', '>', 100)->get();
$users = DB::table('users')
              ->where('votes', '>', 100)
              ->orWhere('name', 'John')
              ->get();
$users = DB::table('users')
      ->whereBetween('votes', [1, 100])->get();
$users = DB::table('users')
      ->whereNotBetween('votes', [1, 100])->get();
$users = DB::table('users')
      ->whereIn('id', [1, 2, 3])->get();
$users = DB::table('users')
      ->whereNotIn('id', [1, 2, 3])->get();
$users = DB::table('users')
      ->whereNull('updated_at')->get();
DB::table('name')->whereNotNull('column')->get();
// 动态的 Where 字段
$admin = DB::table('users')->whereId(1)->first();
$john = DB::table('users')
      ->whereIdAndEmail(2, 'john@doe.com')
      ->first();
$jane = DB::table('users')
      ->whereNameOrAge('Jane', 22)
      ->first();
// Order By, Group By, 和 Having
$users = DB::table('users')
      ->orderBy('name', 'desc')
      ->groupBy('count')
      ->having('count', '>', 100)
      ->get();
DB::table('name')->orderBy('column')->get();
DB::table('name')->orderBy('column','desc')->get();
DB::table('name')->having('count', '>', 100)->get();
// 偏移 & 限制
$users = DB::table('users')->skip(10)->take(5)->get();
```

### Joins 

```
// 基本的 Join 声明语句
DB::table('users')
    ->join('contacts', 'users.id', '=', 'contacts.user_id')
    ->join('orders', 'users.id', '=', 'orders.user_id')
    ->select('users.id', 'contacts.phone', 'orders.price')
    ->get();
// Left Join 声明语句
DB::table('users')
->leftJoin('posts', 'users.id', '=', 'posts.user_id')
->get();
// select * from users where name = 'John' or (votes > 100 and title <> 'Admin')
DB::table('users')
    ->where('name', '=', 'John')
    ->orWhere(function($query) {
        $query->where('votes', '>', 100)
              ->where('title', '<>', 'Admin');
    })
    ->get();
```

### 聚合 

```
$users = DB::table('users')->count();
$price = DB::table('orders')->max('price');
$price = DB::table('orders')->min('price');
$price = DB::table('orders')->avg('price');
$total = DB::table('users')->sum('votes');
```

### 原始表达句

```
$users = DB::table('users')
                   ->select(DB::raw('count(*) as user_count, status'))
                   ->where('status', '<>', 1)
                   ->groupBy('status')
                   ->get();
// 返回行
DB::select('select * from users where id = ?', array('value'));
DB::insert('insert into foo set bar=2');
DB::update('update foo set bar=2');
DB::delete('delete from bar');
// 返回 void
DB::statement('update foo set bar=2');
// 在声明语句中加入原始的表达式
DB::table('name')->select(DB::raw('count(*) as count, column2'))->get();
 
```

### Inserts / Updates / Deletes / Unions / Pessimistic Locking

```
// 插入
DB::table('users')->insert(
  ['email' => 'john@example.com', 'votes' => 0]
);
$id = DB::table('users')->insertGetId(
  ['email' => 'john@example.com', 'votes' => 0]
);
DB::table('users')->insert([
  ['email' => 'taylor@example.com', 'votes' => 0],
  ['email' => 'dayle@example.com', 'votes' => 0]
]);
// 更新
DB::table('users')
          ->where('id', 1)
          ->update(['votes' => 1]);
DB::table('users')->increment('votes');
DB::table('users')->increment('votes', 5);
DB::table('users')->decrement('votes');
DB::table('users')->decrement('votes', 5);
DB::table('users')->increment('votes', 1, ['name' => 'John']);
// 删除
DB::table('users')->where('votes', '<', 100)->delete();
DB::table('users')->delete();
DB::table('users')->truncate();
// 集合
 // unionAll() 方法也是可供使用的，调用方式与 union 相似
$first = DB::table('users')->whereNull('first_name');
$users = DB::table('users')->whereNull('last_name')->union($first)->get();
// 消极锁
DB::table('users')->where('votes', '>', 100)->sharedLock()->get();
DB::table('users')->where('votes', '>', 100)->lockForUpdate()->get();
```