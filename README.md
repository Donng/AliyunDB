## aliyun-analytic-db

阿里云分析型数据库的连接层 , 基于laravel5.5实现

### 安装
安装有两种方式：
##### ① 执行命令安装
```bash 
composer require donng/aliyun-analytic-db 
```
##### ② 直接编辑composer.json
```json
require: {
    "donng/aliyun-analytic-db": "^1.4",
}
```
然后运行 ```composer update```

### 配置
##### ① 生成配置文件
```bash
php artisan vendor:publish --provider="Donng\AnalyticDB\Providers\AnalyticDBProvider"
```

##### ② 配置数据库信息
在 .env 文件中配置阿里云的数据库连接和sql记录的数据库连接名称.
> 如果不配置以下两个常量，将连接数据库配置文件中的默认配置。

```
ANALYTIC_CONNECTION=your analytic connection
RECORD_CONNECTION=your record connection
```
##### ③ 数据库迁移（生成sql记录的表 ）
```bash
php artisan migrate
```
  
>生成sql_records表，记录执行的表和运行的时间，默认关闭。如果不需要sql记录功能，####可跳过此步骤。

### 使用
```php
use AnalyticDB;

// 插入记录(无绑定)
$result = AnalyticDB::withoutPrepare()->insert($sql);
// 插入记录(预编译，绑定数据)
$result = AnalyticDB::insert($sql, $bindingArr);

// 获得所有记录
$result = AnalyticDB::select($sql)->get();
// 获得第一条记录
$result = AnalyticDB::select($sql)->first();
// 不记录sql获取数据（可在配置文件中配置record => false 全部禁用记录sql）
$result = AnalyticDB::select($sql)->disableRecord()->get();
```
###### 当前可调用方法
1. ```->select($sql) //输入原生sql```
2. ```->get() // 查询所有记录```
3. ```->first()        // 查询一条记录```
4. ```disableRecord()  // 此条记录禁用记录功能```
5. ```withoutPrepare() // 此条查询不执行预编译```
6. ```insert()         // 插入数据```



