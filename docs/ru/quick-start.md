# Быстрый запуск

Для примера, мы будем использовать таблицу `users`, которая входит в состав дистрибутива `Laravel`, структура таблицы может быть такой:
```sql
CREATE TABLE `users` (
  `id` int(10) unsigned NOT NULL AUTO_INCREMENT,
  `name` varchar(255) COLLATE utf8_unicode_ci NOT NULL,
  `email` varchar(255) COLLATE utf8_unicode_ci NOT NULL,
  `password` varchar(60) COLLATE utf8_unicode_ci NOT NULL,
  `remember_token` varchar(100) COLLATE utf8_unicode_ci DEFAULT NULL,
  `created_at` timestamp NOT NULL DEFAULT '0000-00-00 00:00:00',
  `updated_at` timestamp NOT NULL DEFAULT '0000-00-00 00:00:00',
  PRIMARY KEY (`id`),
  UNIQUE KEY `users_email_unique` (`email`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COLLATE=utf8_unicode_ci
```
Модель для этой таблицы находится в файле `App\User.php`

Что бы настроить `CRUD` интерфейс для таблицы `users` проделайте следующие шаги:

## Добавьте контроллер

Используйте следующую команду что бы создать контроллер для модели `App\User`

```php
php artisan admin:make UserController --model=\\App\\User

// для пользователей windows:
php artisan admin:make UserController --model=App\User

// для Laravel версии 8+:
php artisan admin:make UserController --model= \\App\\Models\\User
```
После выполнения команды, появится контроллер `app/Admin/Controllers/UserController.php`.

## Добавьте маршрут

Добавьте маршрут в файл `app/Admin/routes.php`：
```
$router->resource('demo/users', UserController::class);
```

## Добавьте элемент меню в интерфейс

Откройте `http://localhost:8000/admin/auth/menu`, добавьте элемент в меню, затем обновите страницу, теперь вы можете найти элемент в меню слева.

> Свойство `uri` заполняется относительно полного адреса админ-панели, если Вам необходимо открывать внутренний ресурс, например `http://localhost:8000/admin/demo/users`, можно указать просто `demo/users`. Однако, если Вам нужно указать внешний источник, укажите полный адрес в данном поле, например `http://laravel-admin.org/`.

### Перевод меню

Добавлять заголовки можно через файл перевода.
Для примера для перевода заголовка 'Work Units' нужно внести в файл:

resources/lang/ru/admin.php
```php
...
// использовать нужно строчные буквы, пробелы нужно заменить на _
'menu_titles' => [
    'work_units' => 'рабочие единицы'
],
```

## Создание Bootstap сетки или формы

Далее Вам нужно отредактировать файл `app/Admin/Contollers/UserController.php`, найдите методы `form()` или `grid()` и пропишите свою логику с помощью `model-grid` и `model-form`,подробнее прочтите [model-grid](/ru/model-grid.md) и [model-form](/ru/model-form.md).
