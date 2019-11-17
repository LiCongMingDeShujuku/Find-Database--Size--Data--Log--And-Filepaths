![CLEVER DATA GIT REPO](https://raw.githubusercontent.com/LiCongMingDeShujuku/git-resources/master/0-clever-data-github.png "李聪明的数据库")

# 查找数据库，大小，数据，日志和文件路径
#### Find Database, Size, Data, Log, And Filepaths
**发布-日期: 2017年07月10日 (评论)**

## Contents

- [中文](#中文)
- [English](#English)
- [SQL Logic](#Logic)
- [Build Info](#Build-Info)
- [Author](#Author)
- [License](#License) 


## 中文
这是来获取所有数据文件的数据库名称，数据，日志，大小和文件路径的一些简单的逻辑（logic）。

## English
Here’s some simple logic to get you the database name, data, log, size, and file path for all your data files.

![#](images/find-database-size-data-log-and-filepaths-a.png?raw=true "#")

---
## Logic
```SQL

use master;
set nocount on
 
select
    [database]  = db_name(smf.database_id)
,   [file_id]
,   [type]      = (case [type] when 0 then 'data' when 1 then 'log' when 2 then 'filestream' when 4 then 'fulltext' end)
,   [logical_name]  = smf.name
,   [physical_name]
,   [size]  =   ( 
                case
                    when smf.size * 8 / 1024 / 1024 < 1 then cast(smf.size * 8 / 1024 as varchar) + ' MB'
                    when smf.size * 8 / 2014 / 1024 > 0 then cast(smf.size * 8 / 1024 /1024 as varchar) + ' GB'
                end
                )
from
    sys.master_files smf
order by
    smf.size desc

```

[![WorksEveryTime](https://forthebadge.com/images/badges/60-percent-of-the-time-works-every-time.svg)](https://shitday.de/)

## Build-Info

| Build Quality | Build History |
|--|--|
|<table><tr><td>[![Build-Status](https://ci.appveyor.com/api/projects/status/pjxh5g91jpbh7t84?svg?style=flat-square)](#)</td></tr><tr><td>[![Coverage](https://coveralls.io/repos/github/tygerbytes/ResourceFitness/badge.svg?style=flat-square)](#)</td></tr><tr><td>[![Nuget](https://img.shields.io/nuget/v/TW.Resfit.Core.svg?style=flat-square)](#)</td></tr></table>|<table><tr><td>[![Build history](https://buildstats.info/appveyor/chart/tygerbytes/resourcefitness)](#)</td></tr></table>|

## Author

- **李聪明的数据库 Lee's Clever Data**
- **Mike的数据库宝典 Mikes Database Collection**
- **李聪明的数据库** "Lee Songming"

[![Gist](https://img.shields.io/badge/Gist-李聪明的数据库-<COLOR>.svg)](https://gist.github.com/congmingshuju)
[![Twitter](https://img.shields.io/badge/Twitter-mike的数据库宝典-<COLOR>.svg)](https://twitter.com/mikesdatawork?lang=en)
[![Wordpress](https://img.shields.io/badge/Wordpress-mike的数据库宝典-<COLOR>.svg)](https://mikesdatawork.wordpress.com/)

---
## License
[![LicenseCCSA](https://img.shields.io/badge/License-CreativeCommonsSA-<COLOR>.svg)](https://creativecommons.org/share-your-work/licensing-types-examples/)

![Lee Songming](https://raw.githubusercontent.com/LiCongMingDeShujuku/git-resources/master/1-clever-data-github.png "李聪明的数据库")

