# 对搜索结果进行排序

您能够使用 *sortby* 关键字来对搜索的结果进行排序。排序顺序（*asc*
表示升序排序，*desc*表示降序排序）也能够被指定。

例如：

*events: severity \> normal sortby time desc*

此查询将返回严重程度高于 normal
的事件，按事件发生的时间进行排序（降序）。
