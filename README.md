CODEEX hh task
=

[Ссылка на задание](http://codeex.ru/tests/back-end.pdf)

***

# Начальная настройка:
1. Клонирование репозитория: `git clone https://github.com/artem0071/hh-codeex.git .`
2. Загрузка пакетов: `composer install`
3. Выполнить `php -r "file_exists('.env') || copy('.env.example', '.env');"`
4. Сгенерировать ключ: `php artisan key:generate --ansi`
5. Выполнить `php artisan storage:link`
6. Заполнить поля БД в `.env`
7. Вписать в переменную `DADATA_API_KEY` ключ от DADATA
8. Выполнить `php artisan migrate`


***

# Доступные команды:
1. `php artisan codeex:create` - Выполняет сохранение в хранилище с данными
2. `php artisan codeex:read` - Выполняет чтение записей из хранилища с данными
3. `php artisan codeex:retrieve {id?}` - Выполняет извлечение записи с помощью уникального идентификатора записи
4. `php artisan codeex:update {id?}` - Принимает входные данные и выполняет обновление существующей записи в хранилище с данными с помощью уникального идентификатора записи
5. `php artisan codeex:destroy {id?}` - Выполняет фактическое удаление записи в хранилище с данными с помощью уникального идентификатора записи
6. `php artisan codeex:compose` - Принимает входные данные и автозаполняет пустые поля сущности
7. `php artisan codeex:remove {id?}` - Принимает входные данные и выполняет логическое удаление существующей записи в хранилище с данными с помощью уникального идентификатора записи с заполнением атрибута `date_removed`
8. `php artisan codeex:export` - Принимает входные данные в виде запроса и выполняет потоковое сохранение записей в CSV файл с последующей передачей его на клиентскую часть
9. `php artisan codeex:import {path?}` - Принимает входные данные в виде CSV файла, выполняет потоковую валидацию файла и производит сохранение в хранилище с данными 

Поля {id?} и {path?} - являются опциональными. Если они не указаны явно, то будут запрошены при работе скрипта

***

## Create:
В процессе выполнении данного запроса будут заданы вопросы относительно вводимых данных. Все поля являются обязательными.

Если не возникло ошибок, то запись будет добавлена в БД, а в консоль будет выведен ID созданной записи

## Read:
При выполнении запроса будет выведена таблица со всеми записями в БД

## Retrieve:
Если ID не указан явно, то он будет запрошен в процессе выполнения команды. 

В случае, если запись не найдена, то будет выведена соответствующая запись. Если запись найдена, то будут выведены ее атрибуты в таблице

## Update:
Если ID не указан явно, то он будет запрошен в процессе выполнения команды. 

При выполнении будут заданы вопросы по атрибутам. Если оставить их пустыми, то они не будут изменены

## Destroy:
Если ID не указан явно, то он будет запрошен в процессе выполнения команды. 

В случае, если запись с текущим ID создана, то она будет удалена из БД

## Compose:
Принимает 2 атрибута:
1) Название
2) Адрес

Оба - опциональны. Остальные поля будут заполнены автоматически и добавлены в БД

## Remove:
Если ID не указан явно, то он будет запрошен в процессе выполнения команды. 

В случае, если запись с текущим ID создана, то она будет помечена в атрибуте `date_removed`

## Export:
Заполняется как и в случае `Create`, но будет создан файл `.csv` в папке `storage/app/public`.
При удачном выполнении будет выведен полный путь к файлу и ссылка на него. Чтобы перейти по ней, необходимо чтобы сервер работал (`php artisan serve`)

## Import:
Импортирует файл `.csv`
Должен быть заполнен в том же формате как выводит файл команда `Export`. Так же должны быть приведены заголовки
