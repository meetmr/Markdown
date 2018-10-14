# Laravel学习笔记03-模板继承和引用

标签（空格分隔）： 继承 引用

---

## 一. 模板继承
- 在目录`resources\views\`下创建文件夹`layout`,该文件夹下面创建模板文件，保留公共部分，删除不公共的部分在该位置写入`@yield('content');`
```
...公共的部分...
@yield('content')
...公共的部分...
```
- 在其他界面，删除公共部分，在头部写入：
```
@extends("layout.main")

@section("content")
    ...不公共的部分...
@endsection
```
## 二. 引用模板
- 从`main.blade.php`里面分离出`nav` `footer`等代码，创建`nav.blade.php`文件将对应代码剪切进去，在`main.blade.php`对应位置通过`@include("layout.nav")`引入模板。





