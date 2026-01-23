---
icon: material/notebook
---

# Use the Index, Luke!笔记

说是笔记，实际上更像是记录雷点，方便以后遇到坑来查阅。相关更容易做成卡片的知识点我全部都是放在了 SuperMemo 进行间隔重复了。

Oracle 创建索引后应该进行的一些维护操作：

> Statistics for a function-based index (FBI) are also kept on table level as virtual columns. Although the Oracle database collects the index statistics for new indexes automatically (since release 10g), it does not update the table statistics. For this reason, the Oracle documentation recommends updating the table statistics after creating a function-based index  
基于函数的索引（function-based index，FBI）的统计信息同样是在表级别维护的，以虚拟列（virtual columns）的形式存在。
尽管 Oracle 数据库会自动收集新建索引的索引统计信息（自 10g 版本起），但它不会自动更新表统计信息。
因此，Oracle 官方文档建议在创建基于函数的索引之后，手动更新表统计信息  
来自[Case-Insensitive-Search](https://use-the-index-luke.com/sql/where-clause/functions/case-insensitive-search)

---

> Tip  
Sometimes ORM tools use UPPER and LOWER without the developer’s knowledge. Hibernate, for example, injects an implicit LOWER for case-insensitive searches.  
有时 ORM 工具会在开发者不知情的情况下使用 UPPER 或 LOWER。例如，Hibernate 会在进行不区分大小写的搜索时，隐式地注入一个 LOWER 调用。  
来自[Over-Indexing](https://use-the-index-luke.com/sql/where-clause/functions/over-indexing)

这可能导致创的索引没被使用（因为索引区分大小写）

---

>
```
SELECT first_name, last_name, subsidiary_id, employee_id
  FROM employees
 WHERE ( subsidiary_id    = :sub_id OR :sub_id IS NULL )
   AND ( employee_id      = :emp_id OR :emp_id IS NULL )
   AND ( UPPER(last_name) = :name   OR :name   IS NULL )
```
该查询为了提高可读性使用了命名绑定变量。所有可能的过滤条件都被静态地写入了 SQL 语句中。只要某个过滤条件不需要，就传入 NULL 作为搜索值：通过 OR 逻辑将该条件“关闭”。
从语法和语义上看，这是一条完全合理的 SQL 语句。NULL 的使用甚至也符合 SQL 三值逻辑（three-valued logic）的定义。然而，它却是性能最差的反模式（performance anti-pattern）之一。
由于任何一个过滤条件都可能在运行时被“取消”，数据库无法针对某个特定过滤条件来优化执行计划。数据库只能为最坏情况做准备——即所有过滤条件都被禁用  
来自[Smart Logic](https://use-the-index-luke.com/sql/where-clause/obfuscation/smart-logic)   

静态 SQL：固定的 SQL 文本，除了绑定变量可变  
动态 SQL：SQL 文本是进行拼接（变量拼接也属于拼接文本）  
因为优化器的判断，静态 SQL 不一定能获得更好的执行计划，从而反而比用动态 SQL 的处理方案慢。
---

> Nevertheless there is a widely used practice that avoids dynamic SQL in favor of static SQL—often because of the “dynamic SQL is slow” myth. This practice does more harm than good if the database uses a shared execution plan cache like Db2 (LUW), the Oracle database, or SQL Server.
尽管（数据库是为动态SQL优化）如此，仍然有一种被广泛采用的做法：为了避免动态 SQL 而使用静态 SQL（static SQL）——这通常源于“动态 SQL 很慢（dynamic SQL is slow）”这一 myth。如果数据库使用共享执行计划缓存（shared execution plan cache）（例如 Db2（LUW）、Oracle 数据库或 SQL Server），这种做法往往弊大于利。  
来自[Smart Logic](https://use-the-index-luke.com/sql/where-clause/obfuscation/smart-logic)   


