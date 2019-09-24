```
// 输出内容，被转义过的
{{ $var }}
// 输出未转义内容
{!! $var !!}
{{-- Blade 注释，不会被输出到页面中 --}}
// 三元表达式的简写，以下相当于「isset($name) ? $name : 'Default'」
{{ $name ?? 'Default' }}
// 等同 echo json_encode($array);
@json($array);
// 禁用 HTML 实体双重编码
Blade::withoutDoubleEncoding();
// 书写 PHP 代码
@php 
@endphp
@csrf // CSRF 域
@method('PUT') // HTML 表单伪造方法 _method
// 服务容器注入，后调用 {{ $metrics->monthlyRevenue() }}
@inject('metrics', 'App\Services\MetricsService')
```

### 包含和继承

```
// 扩展布局模板
@extends('layout.name')
// 区块占位
@yield('name')
// 第一种、直接填入扩展内容
@section('title',  'Page Title')
// 第二种、实现命名为 name 的区块（yield 占位的地方）
@section('sidebar')
	// 继承父模板内容
	@parent
@endsection
// 可继承内容区块
@section('sidebar')
@show
// 继承父模板内容（@show 的区块内容）
@parent
// 包含子视图
@include('view.name')
// 包含子视图，并传参
@include('view.name', ['key' => 'value']);
@includeIf('view.name',  ['some'  =>  'data'])
@includeWhen($boolean,  'view.name',  ['some'  =>  'data'])
// 包含给定视图数组中第一个存在的视图
@includeFirst(['custom.admin',  'admin'],  ['some'  =>  'data'])
// 加载本地化语句
@lang('messages.name')
@choice('messages.name', 1);
// 检查片断是否存在
@hasSection('navigation')
        @yield('navigation')
@endif
// 迭代 jobs 数组并包含
@each('view.name',  $jobs,  'job')
@each('view.name',  $jobs,  'job',  'view.empty')
// 堆栈
@stack('scripts')
@push('scripts')
    <script src="/example.js"></script>
@endpush
// 栈顶插入
@prepend('scripts')
@endprepend
// 组件
@component('alert', ['foo' => 'bar'])
    @slot('title')
    @endslot
@endcomponent
// 注册别名 @alert(['type' => 'danger'])...@endalert
Blade::component('components.alert',  'alert');
```

### 条件语句

```
@if (count($records) === 1)
@elseif  (count($records) > 1)
@else
@endif
// 登录情况下
@unless (Auth::check())
@endunless
// $records 被定义且不是  null...
@isset($records)
@endisset
// $records 为空...
@empty($records)
@endempty
// 此用户身份已验证...
@auth // 或 @auth('admin')
@endauth
// 此用户身份未验证...
@guest // 或 @guest('admin')
@endguest
@switch($i)
    @case(1)
        @break
    @default
        // 默认
@endswitch
```

### 循环

```
// for 循环
@for ($i = 0; $i < 10; $i++)
@endfor
// foreach 迭代
@foreach ($users as $user)
@endforeach
// 迭代如果为空的话
@forelse ($users as $user)
@empty
@endforelse
// while 循环
@while (true)
@endwhile
// 终结循环
@continue
@continue($user->type  ==  1) // 带条件
// 跳过本次迭代
@break
@break($user->number  ==  5) // 带条件
// 循环变量
$loop->index 		// 当前迭代的索引（从 0 开始计数）。
$loop->iteration 	// 当前循环迭代 (从 1 开始计算）。
$loop->remaining 	// 循环中剩余迭代的数量。
$loop->count 		// 被迭代的数组元素的总数。
$loop->first 		// 是否为循环的第一次迭代。
$loop->last 		// 是否为循环的最后一次迭代。
$loop->depth 		// 当前迭代的嵌套深度级数。
$loop->parent 		// 嵌套循环中，父循环的循环变量
```

### JavaScript 代码

```
// JS 框架，保留双大括号，以下会编译为 {{ name }}
@{{ name }}
// 大段 JavaScript 变量，verbatim 里模板引擎将不解析
@verbatim
        Hello, {{ javascriptVariableName }}.
@endverbatim
```

