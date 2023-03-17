# Fat-Free Framework

## Databases

### MySQL

- Throw exceptions on errors
- Enforce complete Unicode support
- Set time zone to UTC

```php
try {
    $dsn = sprintf('mysql:dbname=%s;host=%s;charset=utf8mb4', getenv('MYSQL_TABLE'), getenv('MYSQL_HOST'));

    $sql = new SQL($dsn, getenv('MYSQL_LOGIN'), getenv('MYSQL_PASSWORD'), [
        PDO::ATTR_ERRMODE => PDO::ERRMODE_EXCEPTION,
    ]);

    $sql->exec("SET NAMES 'utf8mb4'");
    $sql->exec("SET time_zone = '+00:00'");

    unset($dsn);
}

catch (PDOException $e) {
    $log->critical("Can't connect to database.", ['message' => $e->getMessage()]);
    $f3->error(503);
}
```

A second solution to enable the exception mode:

```php
$sql->pdo()->setAttribute(PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION);
```
