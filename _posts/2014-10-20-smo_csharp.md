---
layout: default
title: 使用SMO导出sql server 2008 R2数据库的架构与脚本
---

# {{ page.title }}

最近的一个新项目用的是SQL SERVER 2008 R2数据库，我需要把其中的结构和数据备份成SQL脚本，方便添加到GIT库，也方便对比每次修改的区别。但使用SQL SERVER 2008 R2自身的导出工具需要人工点，而且有几个选项也需要改，有点费事。于是我查了下，发现可以用SMO来做一个小工具，自动把数据库的架构和表中的数据导出为SQL脚本。

网上搜到的关于SMO的资料不是太多，不过也不是太复杂。按后面的参考资料来做，基本没什么大问题。记录下我遇到的几个问题：

1. 添加引用。在Visual Studio 2010里选项添加.net控件的引用，找不到Microsoft.SqlServer.*，于是直接添加DLL。
2. 我装的是中文版SQL SERVER 2008 R2，在导出时看到的选项全是中文的，但网上能找到的MSDN的帮助里对这些选项的解释又是英文的，更烦的是SMO的Options里使用的选项名与这些英文名还不是直接的对应关系。只能连猜带试了。例如“编写排序规则脚本”对应的是Scripter.Options.NoCollation = false。
3. 在导出脚本时要使用Scripter.Script()，而如果是导出数据，则要使用Scripter.EnumScript()。

仍不明确的问题：

- Scripter.Options.Dri*选项有什么含义？例如scripter.Options.DriIndexes和scripter.Options.Indexes有什么区别？

![SMO_Scripter]({{ site.baseurl }}images/SMO_Scripter.jpg)

## 参考资料

- http://blogs.technet.com/b/heyscriptingguy/archive/2010/11/04/use-powershell-to-script-sql-database-objects.aspx
- http://msdn.microsoft.com/zh-cn/vstudio/bb895179(v=sql.90).aspx
- http://www.codeproject.com/Articles/13755/SMO-Manage-your-SQL-Server
- SQL Server编程系列(1):SMO介绍 http://blog.csdn.net/zhoufoxcn/article/details/7574658

-------------------------------------------------------------
{{ page.date | date_to_string }}