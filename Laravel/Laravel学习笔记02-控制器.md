# Laravel学习笔记02-控制器

标签（空格分隔）： 控制器 

---
## 一. 控制器的创建
- 命令行:
```
php artisan make:controller PostController
```
## 二. 视图的创建
- 在控制器当中，设置视图渲染。使用`view()`函数，第一个参数为视图地址，第二个参数为要传递进去的数组。
```
//文章列表
    private function index(){
		return view('posts/index');
	}
```
- 在目录`resources\views\`下创建`posts`文件夹，在该文件夹下创建`index.blade.php`模板文件。
- 然后通过设置的路由访问`http://域名/posts`
## 三. 模板参数传递
- 控制器代码
```
//文章详情
public function show(){
	return view('posts/show',['title'=>'参数传递测试']);
}
```
- 模板代码
```
<h2 class="blog-post-title">{{$title}}</h2>
```
#### compact()参数传递
- 使用`compact()`来传递参数:
```
public function index(){
    	$posts = [
    		[
    			'title'=>'标题1',
				'content'=>'中文1中文1中文1中文1中文1中文1中文1中文1中文1'
			],[
				'title'=>'标题2',
				'content'=>'中文2中文2中文2中文2中文2中文2中文2中文2中文2'
			],[
				'title'=>'标题3',
				'content'=>'中文3中文3中文3中文3中文3中文3中文3中文3中文3'
			],[
				'title'=>'标题4',
				'content'=>'中文4中文4中文4中文4中文4中文4中文4中文4中文4'
			]
		];
		return view('posts/index',compact('posts'));
	}
```
## 四. 模板使用函数
### 1. if()
- 控制器代码。这里传递一个`isShow`
```
//文章详情
	public function show(){
		return view('posts/show',['title'=>'参数传递测试','isShow'=>false]);
	}
```
- 模板代码。使用`@if()`,切记在最后结束时要用`$endif`
```
@if($isShow == true)
<p>这里是普通的html代码</p>
@endif
```
### 2. foreach()
- 控制器代码
```
//文章列表
public function index(){
	$posts = [
		[
			'title'=>'标题1',
			'content'=>'中文1中文1中文1中文1中文1中文1中文1中文1'
		],[
			'title'=>'标题2',
			'content'=>'中文2中文2中文2中文2中文2中文2中文2中文2'
		],[
			'title'=>'标题3',
			'content'=>'中文3中文3中文3中文3中文3中文3中文3中文3'
		],[
			'title'=>'标题4',
			'content'=>'中文4中文4中文4中文4中文4中文4中文4中文4'
		]
	];
	return view('posts/index',['posts'=>$posts]);
}
```
- 模板代码
```
@foreach($posts as $post)
<div>
    <h2>{{$post['title']}}</h2>
    <p>{{$post['content']}}...</p>
</div>
@endforeach
```





