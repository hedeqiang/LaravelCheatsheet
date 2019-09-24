```
// 自动处理分页逻辑
Model::paginate(15);
Model::where('cars', 2)->paginate(15);
// 使用简单模板 - 只有 "上一页" 或 "下一页" 链接
Model::where('cars', 2)->simplePaginate(15);
// 手动分页
Paginator::make($items, $totalItems, $perPage);
// 在页面打印分页导航栏
$variable->links();

// 获取当前页数据数量。
$results->count()
// 获取当前页页码。
$results->currentPage()
// 获取结果集中第一条数据的结果编号。
$results->firstItem()
// 获取分页器选项。
$results->getOptions()
// 创建分页 URL 范围。
$results->getUrlRange($start, $end)
// 是否有多页。
$results->hasMorePages()
// 获取结果集中最后一条数据的结果编号。
$results->lastItem()
// 获取最后一页的页码（在 `simplePaginate` 中无效）。
$results->lastPage()
// 获取下一页的 URL 。
$results->nextPageUrl()
// 当前而是否为第一页。
$results->onFirstPage()
// 每页的数据条数。
$results->perPage()
// 获取前一页的 URL。
$results->previousPageUrl()
// 数据总数（在 `simplePaginate` 无效）。
$results->total()
// 获取指定页的 URL。
$results->url($page)
```