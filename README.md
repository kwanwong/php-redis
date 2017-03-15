# 分布式中使用redis实现SESSION共享

*设置SESSION*
```php
ini_set("session.save_handler", "redis");
ini_set("session.save_path", "tcp://192.168.2.253:6379");

session_start();

//存入session
$_SESSION['session_name'] = '123456';
```

*获取SESSION*
```php
//连接redis
$redis = new redis();
$redis->connect('192.168.2.253', 6379);

//检查session_id
echo 'session_id:' . session_id() . '<br/>';

//redis存入的session（redis用session_id作为key,以string的形式存储）
$redis->get('PHPREDIS_SESSION:' . session_id());
```