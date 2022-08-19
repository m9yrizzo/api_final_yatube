# Yatube
## Описание
Благодаря этому проекту можно будет делится историями и мыслями.

Пользователю доступно:
- Публикация постов
- Обединение постов по тематике (группы)
- Подписки на других авторов
- Комментирование постов 

API позволит взаимодействоваnь другим приложениям и сервисам с Yatube.
Все стандартные действия Yatube могут стать доступными через Ваш клиент/

### Технологии
- Python 3.7
- Django 2.2.19

## Установка
Клонировать репозиторий и перейти в него в командной строке:
```
  git clone https://github.com/m9yrizzo/api_final_yatube.git
```
```
  cd kittygram
```
Cоздать и активировать виртуальное окружение:
```
  python3 -m venv env
```
```
  source env/bin/activate
```
Установить зависимости из файла requirements.txt:
```
  python3 -m pip install --upgrade pip
```
```
  pip install -r requirements.txt
```
Выполнить миграции:
```
  python3 manage.py migrate
```
Запустить проект:
```
  python3 manage.py runserver
```
## Примеры запросов к API.
*По endpoint ```/redoc``` доступны все возможные примеры запросов и наиболее вероятные ответы API.
Далее представлены некоторые из них.*

### Создание публикации
Добавление новой публикации в коллекцию публикаций. Анонимные запросы запрещены.
```
http://127.0.0.1:8000/api/v1/posts/
```

REQUEST BODY SCHEMA: application/json
  
| Field  | Type |
| ------------- | ------------- |
| text **(required)**  | string (текст публикации)  |
| image  | string or null <binary>  |
| group  | integer or null (id сообщества)  |

```
{
  "text": "string",
  "image": "string",
  "group": 0
}  
```
* * *
  
Responses:
- 201 Удачное выполнение запроса
  
  REQUEST BODY SCHEMA: application/json
  
  | Field  | Type |
  | ------------- | ------------- |
  | id  | integer (id публикации)  |
  | author  | string (username пользователя)  |
  | text **(required)**  | string (текст публикации)  |
  | pub_date  | string <date-time>  |
  | image  | string or null <binary>  |
  | group  | integer or null (id сообщества)  |

  ```
  {
    "id": 0,
    "author": "string",
    "text": "string",
    "pub_date": "2019-08-24T14:15:22Z",
    "image": "string",
    "group": 0
    } 
  ```
* * *  
- 400 Отсутствует обязательное поле в теле запроса
  
  ```
  {
   - "text": [
       "Обязательное поле."
     ]
  }
  ```
* * *
- 401 Запрос от имени анонимного пользователя
  
  ```
  {
    "detail": "Учетные данные не были предоставлены."
  } 
  ```
* * *

### Список сообществ
Получение списка доступных сообществ.
```
http://127.0.0.1:8000/api/v1/groups/
```
Responses:
- 201 Удачное выполнение запроса
  
  REQUEST BODY SCHEMA: application/json
  
  | Field  | Type |
  | ------------- | ------------- |
  | id  | integer  |
  | title **(required)**  | string (<= 200 characters)  |
  | slug **(required)**  | string (<= 50 characters ^[-a-zA-Z0-9_]+$)  |
  | description **(required)**  | string  |

  ```
  [
    {
      "id": 0,
      "title": "string",
      "slug": "string",
      "description": "string"
    }
  ]  
  ```
* * *

### Авторы
**ЯПрактикум** + немного ```m9yrizo```
