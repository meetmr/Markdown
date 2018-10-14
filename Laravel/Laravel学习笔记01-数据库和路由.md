# Laravel学习笔记01-数据库和路由

标签（空格分隔）： Laravel 数据库

---
## 一. 数据库
### 1. 数据库配置文件
- 在`config/database.php`文件里面`'default' => env('DB_CONNECTION', 'mysql'),`标明了用途，可以在laravel根目录下的`.env`文件里面配置对应的数据库信息。
```
DB_CONNECTION=mysql
DB_HOST=127.0.0.1
DB_PORT=3306
DB_DATABASE=dbname
DB_USERNAME=username
DB_PASSWORD=userpaw
```

### 2. 校验数据库是否连接
- 在当前项目目录执行以下命令可使用当前的项目数据库配置信息在数据库里创建一个`migrate`表。
```
php artisan migrate:install
```

## 二. 路由
### 1.路由的配置的文件
- 在`routes`文件夹下的`web.php`文件里。默认会有一个默认的欢迎页面路由。
```
Route::get('/', function () {
    return view('welcome');
});
```
### 2.路由语法和案例
- get路由类型
- - 语法
```
Route:get('/','[命名空间+控制器名]@[函数名]');
```
- - 案例
- - - 例如我现在在`/App/Http/Controllers`下有一个控制器`LoginSystem`,有`index()`和`exit()`函数用于控制用户的登录和退出。
```
Route:get('/login','/App/Http/Controllers/LoginSystem@index');
//修改后访问路由为 http://域名/login
Route:get('/exit','/App/Http/Controllers/LoginSystem@exit');
//修改后访问路由为 http://域名/exit
```

> 注意事项:命名空间和控制器名必须严格按照大小写(规范要求)
### 3.Laravel的所有方法
```
Route:get($url,$callback);
//主要用于获取资源
Route:post($url,$callback);
//用于创建资源
Route:put($url,$callback);
//更新资源
Route:patch($url,$callback);
//增量更新资源
Route:delete($url,$callback);
//删除资源
Route:options($url,$callback);
//查询资源支持的方法
```
> 注意:在开发中请严格设置不同的路由(规范要求)

### 4.路由的使用
#### ① 常规使用get或者post
- 现有路由。用于创建用户
```
Route:post('/create','/App/Http/Controllers/User@create');
```
- HTML代码。提交表单
```
<form action="/create" method="POST">
...
</form>
```
#### ② 特殊使用put
- 路由
```
Route:put('/create','/App/Http/Controllers/User@create');
```
- HTML。这里有两种方法，等价
```
<form action="/create" method="POST">
    <input type="hidden" name="_method" value="PUT">
    <!--或者使用-->
    {{ method_field("PUT") }}
    ...
</form>
```


### 5.其他路由函数
```
Route:any();
//只要符合，那就匹配所有的类型(get post put ...)
Route:match(['get','post'],'/create','/App/Http/Controllers/User@create')；
//指定要支持是get还是post，这个只能支持get和post
```

### 6.路由参数
- 路由设置
```
Route:get('/goods/{id}','/App/Http/Controllers/Goods@index');
```
- 函数
```
function index($id){
    ...
}
```
### 7.路由分组
- 路由分组使用` Route:group() `
- 例如，现有`Massage`控制器，有如下路由:
```
Route:get('/massage/del/{id}','/App/Http/Controllers/Massage@delete');
Route:get('/massage/cre','/App/Http/Controllers/Massage@create');
Route:get('/massage/sel/{id}','/App/Http/Controllers/Massage@select');
```
- 现在使用路由分组，改为:
```
Route:group(['prefix'=>'massage'],function(){
   Route:get('/del/{id}','/App/Http/Controllers/Massage@delete');
    Route:get('/cre','/App/Http/Controllers/Massage@create');
    Route:get('/sel/{id}','/App/Http/Controllers/Massage@select'); 
});
```

### 8.绑定模型
- 现有模型`message`，设置路由往里面传递参数。
```
Route:get('/message/{post}','/App/Http/Controllers/Massage@show');
```
- PHP代码。这样就传递过来了模型和模型的参数
```
function show(\App\Post $post){
    ...
}
```




























