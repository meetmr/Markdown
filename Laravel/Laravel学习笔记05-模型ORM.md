# Laravel学习笔记05-模型ORM

标签（空格分隔）： ORM

---

## 一、创建模型
- 模型文件地址:`App\Http\`
- 使用命令创建模型
```
php artisan make:model Post
```
- 如果模型文件内什么不指定表名，那么默认对应表名的复数 `Posts`表
- 使用`protected $table=""`指定表名，例如:
```
protected $table="table2";
```
## 二、使用thinker工具

> thinker工具在不创建交互界面的情况下对数据库进行操作

- 启动thinker
```
php artisan thinker
```
### 1.案例:往文章表`Posts`表内写入对应数据。字段:title,content
```
>>> $post = new App\Post();
=> App\Post {#2806}
>>> $post->title = "this is post1"
=> "this is post1"
>>> $post->content = "this is post content"
=> "this is post content"
>>> $post->save();
=> true
```
- 创建完成发现`create_at`和`update_at`的时间不对，这是因为Larvalel的时区在英国，我们需要修改时区。
- 打开`config\app.php`，找到大约67行的位置`timezone`的参数改为`Asia/Shanghai`。然后重启thinker继续输入。
### 2.在thinker中操作数据库
- 使用find()主键查询
```
$post->find(1);
//find中直接查询主键id
```
- 使用where()条件查询
```
$post->where("title","this is post1")->first();
//first()返回数据
$post->where("title","this is post1")->get();
//get()方式返回的是一个Collection对象
```
- 更新数据
```
>>> $post->find(2);
=> App\Post {#2802
     id: 2,
     title: "Title1",
     content: "Content1",
     user_id: 0,
     created_at: "2018-10-19 09:12:20",
     updated_at: "2018-10-19 09:12:20",
   }
>>> $post->title="updateTitle"
=> "updateTitle"
>>> $post->save();
=> true
```
- 删除数据
```
>>> $post->find(2);
=> App\Post {#2809
     id: 2,
     title: "updateTitle",
     content: "Content1",
     user_id: 0,
     created_at: "2018-10-19 09:12:20",
     updated_at: "2018-10-19 09:13:03",
   }
>>> $post->delete();
=> true
```



