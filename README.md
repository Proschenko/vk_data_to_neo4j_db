# Get-Vk-Info-NoSQL_DB-Query

## Описание
Консольное приложение vk_info_fetcher.py использует VK API для получения информации о пользователе ВКонтакте, его фолловерах, подписках и группах. Приложение сохраняет результаты в NoSQL базе данных Neo4j. Также консольное приложение Neo4jQueries.py позволяет делать запросы к NoSQL базе данных Neo4j.

## Требования
- Python 3.6+
- Библиотека `requests`
- Библиотека `neo4j`
- Библиотека `py2neo`
- Access-токен VK для авторизации

## 1. Клонирование репозитория

Склонируйте репозиторий с приложением:

```bash
git clone  https://github.com/Proschenko/vk_api_to_neo4j_base.git
cd Ваш_Путь_До_Репозитория\vk_api_to_neo4j_base
```

## 2. Установка зависимостей

После клонирования репозитория, перейдите в директорию проекта и установите необходимые зависимости с помощью pip:

```bash
pip install -r requirements.txt
```

## 2. Создание переменной окружения

(Запустите консоль от имени администратора!) Для того чтобы приложение могло подключиться к VK API, необходимо создать переменную окружения VK_TOKEN. Вставьте ваш токен доступа ВК:

Windows:
```bash
set VK_TOKEN=ваш_токен_доступа
```

Linux/MacOS:
```bash
export VK_TOKEN="ваш_токен_доступа"
```

## 4. Создание базы данных NoSQL neo4j

Запустите приложение, указав ID пользователя ВК (опционально) и путь для сохранения результата (опционально). Если ID пользователя не указан, будет использоваться ID по умолчанию.

Пример для Windows:
```bash
python путь_до_репозитория\vk_api_to_neo4j_base\vk_info_fetcher.py --user_id 1 
```

Пример для Linux/MacOS:
```bash
python путь_до_репозитория\vk_api_to_neo4j_base\vk_info_fetcher.py --user_id 1 
```

## 5. Результаты

После успешного выполнения приложения vk_info_fetcher.py результаты будут сохранены в neo4j базу. БД будет содержать следующую информацию:

    Пользователей и их связи(фолловеров)
    Группы и их связи(подписчики)

## 6. Выполнение запросов

Теперь можно выполнить запросы к базе данных. Это делается следующим образом:

```bash
python путь_до_репозитория\vk_api_to_neo4j_base\Neo4jQueries.py --query <тип_запроса> [--limit <количество>]
```
--query — обязательный аргумент, который задаёт тип запроса к базе данных. Доступные значения:

    count_users — подсчитывает общее количество пользователей.
    count_groups — подсчитывает общее количество групп.
    top_users — выводит пользователей с наибольшим количеством подписчиков.
    top_groups — выводит группы с наибольшим количеством подписчиков.
    mutual_followers — находит пользователей, которые взаимно подписаны друг на друга.

--limit — необязательный параметр, который определяет, сколько записей будет возвращено для запросов top_users и top_groups. По умолчанию установлено значение 5, но можно указать любое количество.

# Вот несколько примеров запросов:

Чтобы получить общее количество пользователей в базе данных:
```bash
python Neo4jQueries.py --query count_users
```

Чтобы получить общее количество групп в базе данных:
```bash
python Neo4jQueries.py --query count_groups
```

Чтобы вывести топ-5 пользователей по числу подписчиков:
```bash
python Neo4jQueries.py --query top_users
```

Чтобы вывести топ-10 пользователей, добавьте параметр --limit:
```bash
python Neo4jQueries.py --query top_users --limit 10
```

Чтобы вывести топ-5 групп по количеству подписчиков:
```bash
python Neo4jQueries.py --query top_groups
```

Чтобы найти пользователей, у которых есть взаимные подписки:
```bash
python Neo4jQueries.py --query mutual_followers
```

## 7. Завершение работы

После выполнения запроса скрипт автоматически закроет соединение с базой данных и завершит работу.
