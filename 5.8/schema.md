# Schema

---

```
// 创建指定数据表
 Schema::create('table', function($table)
{
  $table->increments('id');
});
// 指定一个连接
 Schema::connection('foo')->create('table', function($table){});
// 通过给定的名称来重命名数据表
 Schema::rename($from, $to);
// 移除指定数据表
 Schema::drop('table');
// 当数据表存在时, 将指定数据表移除
 Schema::dropIfExists('table');
// 判断数据表是否存在
 Schema::hasTable('table');
// 判断数据表是否有该列
 Schema::hasColumn('table', 'column');
// 更新一个已存在的数据表
 Schema::table('table', function($table){});
// 重命名数据表的列
$table->renameColumn('from', 'to');
// 移除指定的数据表列
$table->dropColumn(string|array);
// 指定数据表使用的存储引擎
$table->engine = 'InnoDB';
// 字段顺序，只能在 MySQL 中才能用
$table->string('name')->after('email');
```

### 索引

```
$table->string('column')->unique();
$table->primary('column');
// 创建一个双主键
$table->primary(array('first', 'last'));
$table->unique('column');
$table->unique('column', 'key_name');
// 创建一个双唯一性索引
$table->unique(array('first', 'last'));
$table->unique(array('first', 'last'), 'key_name');
$table->index('column');
$table->index('column', 'key_name');
// 创建一个双索引
$table->index(array('first', 'last'));
$table->index(array('first', 'last'), 'key_name');
$table->dropPrimary(array('column'));
$table->dropPrimary('table_column_primary');
$table->dropUnique(array('column'));
$table->dropUnique('table_column_unique');
$table->dropIndex(array('column'));
$table->dropIndex('table_column_index');
```

### 外键

```php
$table->foreign('user_id')->references('id')->on('users');
$table->foreign('user_id')->references('id')->on('users')->onDelete('cascade'|'restrict'|'set null'|'no action');
$table->foreign('user_id')->references('id')->on('users')->onUpdate('cascade'|'restrict'|'set null'|'no action');
$table->dropForeign(array('user_id'));
$table->dropForeign('posts_user_id_foreign');
```

### 字段类型

```php
// 自增
$table->increments('id');
$table->bigIncrements('id');

// 数字
$table->integer('votes');
$table->tinyInteger('votes');
$table->smallInteger('votes');
$table->mediumInteger('votes');
$table->bigInteger('votes');
$table->float('amount');
$table->double('column', 15, 8);
$table->decimal('amount', 5, 2);

// 字符串和文本
$table->char('name', 4);
$table->string('email');
$table->string('name', 100);
$table->text('description');
$table->mediumText('description');
$table->longText('description');

// 日期和时间
$table->date('created_at');
$table->dateTime('created_at');
$table->time('sunrise');
$table->timestamp('added_on');
// Adds created_at and updated_at columns
 // 添加 created_at 和 updated_at 行
$table->timestamps();
$table->nullableTimestamps();

// 其它类型
$table->binary('data');
$table->boolean('confirmed');
// 为软删除添加 deleted_at 字段
$table->softDeletes();
$table->enum('choices', array('foo', 'bar'));
// 添加 remember_token 为 VARCHAR(100) NULL
$table->rememberToken();
// 添加整型的 parent_id 和字符串类型的 parent_type
$table->morphs('parent');
->nullable()
->default($value)
->unsigned()
```