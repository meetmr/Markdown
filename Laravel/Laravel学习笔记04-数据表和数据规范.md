# Laravel学习笔记04-数据表和数据规范

标签（空格分隔）： 数据库 规范

---

- 在Laravel当中，系统数据规范建议:
-  - 表名:建议为名词的复数形式，例如`posts`
- - 外键:建议名词_id，例如`user_id`
- - 时间:created_at/updated_at

## 一，使用数据迁移创建数据表
- 使用系统提供的命令创建migration文件
- 系统命名规范为:年份_月份_日期_动词_表名_table.php,其中`动词_表名_table`为手动填写，其他为系统自动生成。
```
php artisan make:migration create_posts_table
```
- 在`database\migration`文件夹下有刚创建的migration文件
- migration文件内包含了`up()`和`down()`函数,前者用于执行的时候，后者用户回滚的时候。
### create -> up()
```
public function up()
    {
		Schema::create('posts', function (Blueprint $table) {
			//用于自增
			$table->increments('id');
			//第一个参数为字段名，第二个参数为长度,建议后面都用上default()
			$table->string('title',255)->default();
			$table->text('content');
			$table->integer('user_id')->default(0);
			//这里会自动创建created_at和updated_at字段
			$table->timestamps();

		});
    }
```
### create -> down()
```
public function down()
    {
    	//用于回滚
		Schema::dropIfExists('posts');
    }
```

### 执行migration
- 执行命令
```
php artison migrate
```
- 注意:在执行到这一步的时候如果你没有给string类型的字段指定长度，可能会报错。那么在`App\Providers`的`AppServiceProvider.php`文件中的`boot()`函数下添加以下代码，指定`string`类型的长度。
```
public function boot()
{
    Schema::defaultStringLength(191);
}
```
- 解释:在Laravel5.4之后，String长度被设定为1071，但是数据库最大程度只能是767，所以会报错。但是在5.4之后字符默认编码为`mb4`,就是一个字符占4个Byte，那么在`boot()`函数当中设置长度为191。

