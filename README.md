# docker-server

Предварительно перед началом работы с сервером необходимо установить: **docker**, **ansible**, **make**.

После запуска сервера, его можно будет увидеть по адрессу `http://localhost/`, отобразиться содержимое файла `./www/index.php`.

> Для настройки сервера, необходимо создать файл `./config.yml` по примеру из `./config.yml.example` и выполнить команду `make local-start` или настройки будут взяты по умолчанию из файла примера.

## Характеристики по умолчанию

* workspace:
    * `php`;
    * `composer`;
    * `nodejs`;
    * `npm`.
* Nginx - `nginx:alpine`;
* PHP - `phpdockerio/php72-fpm:latest`;
* MySQL - `mysql:latest`.

## Структура сервера

* `.data` - данные хранящиеся на основной OC и подключаемые в контйнера;
* `ansible` - конфигурационные файлы;
* `service` - подключаемые сервисы;
* `temp` - генерируемые файлы при старте сервера (создаются один раз, если до этого их не было);
* `www` - корневая папка сервера.

## Полезные ссылки

* [localhost:80](http://localhost/);
* [MySql:8081](http://localhost:8081/).

## Сервер

### Запустить

```bash
make local-start
```

### Остановить

```bash
make local-stop
```

### Перезапустить

```bash
make local-restart
```

### Пересобрать

Пересобирает контейра

```bash
make local-rebuild-soft
```

Пересобирает контейра и устанавливает файлы в папке `temp` в изначальное состояние

```bash
make local-rebuild-force
```

### Открыть консоль workspace

```bash
make docker-bash
```

### Посмотреть статус контейнеров

```bash
make docker-status
```

## Настройки

### Просмотреть

#### Список параметров команды

 Название | Тип | Описание
:-------|:-------------|:--------
path | string | Путь до файла настроек

```bash
ansible-vault view --vault-id password <path>
```

#### Пример выполнения команды

```bash
ansible-vault view --vault-id password ansible/vars/global/vault.yml
```

### Расшифровать

#### Список параметров команды

 Название | Тип | Описание
:-------|:-------------|:--------
path | string | Путь до файла настроек

```bash
ansible-vault decrypt --vault-id password <path>
```

#### Пример выполнения команды

```bash
ansible-vault decrypt --vault-id password ansible/vars/global/vault.yml
```

### Зашифровать

#### Список параметров команды

 Название | Тип | Описание
:-------|:-------------|:--------
path | string | Путь до файла настроек

```bash
ansible-vault encrypt --vault-id password <path>
```

#### Пример выполнения команды

```bash
ansible-vault encrypt --vault-id password ansible/vars/global/vault.yml
```