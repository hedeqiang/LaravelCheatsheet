# Collection

---

```php
// 创建集合
collect([1, 2, 3]);
// 返回该集合所代表的底层数组：
$collection->all();
// 返回集合中所有项目的平均值：
collect([1, 1, 2, 4])->avg() // 2
$collection->average();
// 将集合拆成多个给定大小的较小集合：
collect([1, 2, 3, 4, 5])->chunk(2); // [[1,2], [3,4], [5]]
// 将多个数组组成的集合折成单一数组集合：
collect([[1],  [4,  5]])->collapse(); // [1, 4, 5]
// 将一个集合的值作为键，再将另一个集合作为值合并成一个集合
collect(['name', 'age'])->combine(['George', 29]);
// 将给定的 数组 或集合值追加到集合的末尾
collect(['PHP'])->concat(['Laravel']); // ['PHP', 'Laravel']
// 用来判断该集合是否含有指定的项目：
collect(['name' => 'Desk'])->contains('Desk'); // true
collect(['name' => 'Desk'])->contains('name',  'Desk'); // true
// 返回该集合内的项目总数：
$collection->count();
// 交叉连接指定数组或集合的值，返回所有可能排列的笛卡尔积
collect([1, 2])->crossJoin(['a', 'b']); // [[1, 'a'],[1, 'b'],[2, 'a'],[2, 'b']]
// dd($collection) 的另一个写法
collect(['John Doe', 'Jane Doe'])->dd();
// 返回原集合中存在而指定集合中不存在的值
collect([1,  2,  3])->diff([2, 4]); // [1, 3]
// 返回原集合不存在与指定集合的键 / 值对
collect(['color' => 'orange', 'remain' =>  6])->diffAssoc(['color' => 'yellow', 'remain' => 6, 'used' => 6]);  // ['color' => 'orange']
// 返回原集合中存在而指定集合中不存在键所对应的键 / 值对
collect(['one' => 10, 'two' => 20])->diffKeys(['two' => 2, 'four' => 4]); // ['four' => 4]
// 类似于 dd() 方法，但是不会中断
collect(['John Doe', 'Jane Doe'])->dump();
// 遍历集合中的项目，并将之传入给定的回调函数：
$collection = $collection->each(function ($item, $key) {});
// 验证集合中的每一个元素是否通过指定的条件测试
collect([1,  2])->every(function  ($value,  $key)  { return $value > 1; }); // false
// 返回集合中排除指定键的所有项目：
$collection->except(['price', 'discount']);
// 以给定的回调函数筛选集合，只留下那些通过判断测试的项目：
$filtered = $collection->filter(function ($item) {
    return $item > 2;
});
// 返回集合中，第一个通过给定测试的元素：
collect([1, 2, 3, 4])->first(function ($key, $value) {
    return $value > 2;
});
// 将多维集合转为一维集合：
$flattened = $collection->flatten();
// 将集合中的键和对应的数值进行互换：
$flipped = $collection->flip();
// 以键自集合移除掉一个项目：
$collection->forget('name');
// 返回含有可以用来在给定页码显示项目的新集合：
$chunk = $collection->forPage(2, 3);
// 返回给定键的项目。如果该键不存在，则返回 null：
$value = $collection->get('name');
// 根据给定的键替集合内的项目分组：
$grouped = $collection->groupBy('account_id');
// 用来确认集合中是否含有给定的键：
$collection->has('email');
// 用来连接集合中的项目
$collection->implode('product', ', ');
// 移除任何给定数组或集合内所没有的数值：
$intersect = $collection->intersect(['Desk', 'Chair', 'Bookcase']);
// 假如集合是空的，isEmpty 方法会返回 true：
collect([])->isEmpty();
// 以给定键的值作为集合项目的键：
$keyed = $collection->keyBy('product_id');
// 传入回调函数，该函数会返回集合的键的值：
$keyed = $collection->keyBy(function ($item) {
    return strtoupper($item['product_id']);
});
// 返回该集合所有的键：
$keys = $collection->keys();
// 返回集合中，最后一个通过给定测试的元素：
$collection->last();
// 遍历整个集合并将每一个数值传入给定的回调函数：
$multiplied = $collection->map(function ($item, $key) {
    return $item * 2;
});
// 返回给定键的最大值：
$max = collect([['foo' => 10], ['foo' => 20]])->max('foo');
$max = collect([1, 2, 3, 4, 5])->max();
// 将给定的数组合并进集合：
$merged = $collection->merge(['price' => 100, 'discount' => false]);
// 返回给定键的最小值：
$min = collect([['foo' => 10], ['foo' => 20]])->min('foo');
$min = collect([1, 2, 3, 4, 5])->min();
// 返回集合中指定键的所有项目：
$filtered = $collection->only(['product_id', 'name']);
// 获取所有集合中给定键的值：
$plucked = $collection->pluck('name');
// 移除并返回集合最后一个项目：
$collection->pop();
// 在集合前面增加一个项目：
$collection->prepend(0);
// 传递第二个参数来设置前置项目的键：
$collection->prepend(0, 'zero');
// 以键从集合中移除并返回一个项目：
$collection->pull('name');
// 附加一个项目到集合后面：
$collection->push(5);
// put 在集合内设置一个给定键和数值：
$collection->put('price', 100);
// 从集合中随机返回一个项目：
$collection->random();
// 传入一个整数到 random。如果该整数大于 1，则会返回一个集合：
$random = $collection->random(3);
// 会将每次迭代的结果传入到下一次迭代：
$total = $collection->reduce(function ($carry, $item) {
    return $carry + $item;
});
// 以给定的回调函数筛选集合：
$filtered = $collection->reject(function ($item) {
    return $item > 2;
});
// 反转集合内项目的顺序：
$reversed = $collection->reverse();
// 在集合内搜索给定的数值并返回找到的键：
$collection->search(4);
// 移除并返回集合的第一个项目：
$collection->shift();
// 随机排序集合的项目：
$shuffled = $collection->shuffle();
// 返回集合从给定索引开始的一部分切片：
$slice = $collection->slice(4);
// 对集合排序：
$sorted = $collection->sort();
// 以给定的键排序集合：
$sorted = $collection->sortBy('price');
// 移除并返回从指定的索引开始的一小切片项目：
$chunk = $collection->splice(2);
// 返回集合内所有项目的总和：
collect([1, 2, 3, 4, 5])->sum();
// 返回有着指定数量项目的集合：
$chunk = $collection->take(3);
// 将集合转换成纯 PHP 数组：
$collection->toArray();
// 将集合转换成 JSON：
$collection->toJson();
// 遍历集合并对集合内每一个项目调用给定的回调函数：
$collection->transform(function ($item, $key) {
    return $item * 2;
});
// 返回集合中所有唯一的项目：
$unique = $collection->unique();
// 返回键重设为连续整数的的新集合：
$values = $collection->values();
// 以一对给定的键／数值筛选集合：
$filtered = $collection->where('price', 100);
// 将集合与给定数组同样索引的值合并在一起：
$zipped = $collection->zip([100, 200]);
```
