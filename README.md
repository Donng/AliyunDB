## aliyun-analytic-db

阿里云分析型数据库的连接层 , 基于laravel5.5实现

### 安装
安装有两种方式：
##### ① 执行命令安装
``` 
composer require donng/aliyun-analytic-db 
```
##### ② 直接编辑composer.json
```
require: {
    "donng/aliyun-analytic-db": "^1.1",
}
```
然后运行 ```composer update```

### 配置
##### ① 生成配置文件
``` 
php artisan vendor:publish --provider="Donng\AnalyticDB\Providers\AnalyticDBProvider"
```
##### ② 生成sql记录的表 
  ```
  php artisan migrate
  ```
  
>生成sql_records表，记录执行的表和运行的时间，默认关闭。如果不需要sql记录功能，####可跳过此步骤。

### 使用
``` 
use AnalyticDB;

$result = AnalyticDB::select($sql)->get();
$result = AnalyticDB::select($sql)->first();
$result = AnalyticDB::select($sql)->disableRecord()->get();
```
###### 当前可调用方法
1. ```->select($sql) //输入原生sql```
2. ```->get() // 查询所有记录```
3. ```->first()        // 查询一条记录```
4. ```disableRecord()  // 此条记录禁用记录功能```
