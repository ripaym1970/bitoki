Yii2 advanced+AdminLTE+раздельная авторизация
---------------------------------------------

Установка локально (Win7, PhpStorm)
------------------
1. В Terminal выполнить инициализацию настроек для разработки:
```
init
```
Выбрать `Developer`

2. Выполняем в `Terminal` установку Yii2:
```
composer install --ignore-platform-reqs
composer update --ignore-platform-reqs
чтобы не удалять 
    "ext-json": "*",
    "ext-posix": "*",
    "ext-zlib": "*",
    "ext-curl": "*",
    "ext-pdo": "*"

```
3. Настроить `common/config/main-local.php`
```
return [
    'components' => [
        'db' => [
            'class' => \yii\db\Connection::class,
            'dsn' => 'mysql:host=localhost;dbname=adv',
            'username' => 'root',
            'password' => '',
            'charset'  => 'utf8',
        
            // Schema cache options (for production environment)
            'emulatePrepare'      => true,
            'schemaCacheDuration' => 60,
            'schemaCache'         => 'cache',
            // Отключить кеширование БД при разработке
            'enableSchemaCache'   => YII_DEBUG ? false : true, 
        ],
    ],
];
```
4. В PhpMyAdmin создаем вручную БД `adv`.
5. В закладке `Database` создаем коннект к БД `adv`.
6. Выполнить в Terminal миграции
```
yii migrate
```
7. Зайти на сайт `admin.dzyga.loc` и выполнить
```
http://admin.dzyga.loc/create/admin
```
Если администратор админки (пользователь с ролью `admin`) существует, то будет редирект на вход в админку.

8. Активируем админа - в PhpMyAdmin в БД `adv` в таблице `user_admin`  для добавленного админа в поле `status` задаем `10`.
```
UPDATE `user_admin` SET `status` = 10 WHERE username = 'имя админа';
```
9. Если нужен новый админ, то надо вручную удалить его в БД из таблицы 'user_admin' командой
```
DELETE FROM `user_admin` WHERE username = 'имя админа';
```
10. 



Обновлять зависимости с помощью Composer
----------------------------------------
```
composer update --ignore-platform-reqs
```

Особенности
-----------

Баги
----
1. Если не грузятся стили - отключить блокировщики рекламы.
