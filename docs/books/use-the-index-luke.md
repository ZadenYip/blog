---
icon: material/notebook
---

# Use the Index, Luke!笔记

说是笔记，实际上更像是记录雷点，方便以后遇到坑来查阅。相关更容易做成卡片的知识点我全部都是放在了 SuperMemo 进行间隔重复了。

> 来自[Over-Indexing](https://use-the-index-luke.com/sql/where-clause/functions/over-indexing)
Tip  
Sometimes ORM tools use UPPER and LOWER without the developer’s knowledge. Hibernate, for example, injects an implicit LOWER for case-insensitive searches.
有时 ORM 工具会在开发者不知情的情况下使用 UPPER 或 LOWER。例如，Hibernate 会在进行不区分大小写的搜索时，隐式地注入一个 LOWER 调用。  

这可能导致创的索引没被使用（因为索引区分大小写）