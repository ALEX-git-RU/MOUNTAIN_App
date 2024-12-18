# Creation Rest API Mountain_App
!virtual internship!
# Этапы работы над созданием мобильного приложения:
    a) Разработка REST API, которое будет обслуживать мобильное приложение;
    b) Разработка мобильного приложения;
    c) Тестирование REST API и мобильного приложения.

1-ый этап - создана база данных, разработан класс по работе с БД и один метод для [REST API](http://127.0.0.1:8000) .

2-ой этап - разработано еще три метода для Rest API;
загружено решение на сервер # ссылка.

3-ий этап - код под тестами, установлена библиотека coverage, также подготовлена [документация](http://127.0.0.1:8000/swagger/?format=openapi), добавлен интерфейс Swagger.

Требования к Rest API

Когда турист поднимется на перевал, он сфотографирует его и внесёт нужную информацию с помощью мобильного приложения:

* координаты объекта и его высоту;
* название объекта;
* несколько фотографий;
* информацию о пользователе, который передал данные о перевале:
* имя пользователя (ФИО строкой);
* почта;
* телефон.

После этого турист нажмёт кнопку «Отправить» в мобильном приложении. Мобильное приложение вызовет метод submitData твоего REST API.

Метод submitData принимает JSON в теле запроса с информацией о перевале. Ниже находится пример такого JSON-а:
~~~
{
  "beauty_title": "пер. ",
  "title": "Пхия",
  "other_titles": "Триев",
  "connect": "", // что соединяет, текстовое поле
 
  "add_time": "2021-09-22 13:18:13",
  "user": {"email": "qwerty@mail.ru", 		
        "fam": "Пупкин",
		 "name": "Василий",
		 "otc": "Иванович",
        "phone": "+7 555 55 55"}, 
 
   "coords":{
  "latitude": "45.3842",
  "longitude": "7.1525",
  "height": "1200"}
 
 
  level:{"winter": "", //Категория трудности. В разное время года перевал может иметь разную категорию трудности
  "summer": "1А",
  "autumn": "1А",
  "spring": ""},
 
   images: [{data:"<картинка1>", title:"Седловина"}, {data:"<картинка>", title:"Подъём"}]
}
~~~
#### Результат метода: JSON

status — код HTTP, целое число:
500 — ошибка при выполнении операции;
400 — Bad Request (при нехватке полей);
200 — успех.
message — строка:
Причина ошибки (если она была);
Отправлено успешно;
Если отправка успешна, дополнительно возвращается id вставленной записи.
id — идентификатор, который был присвоен объекту при добавлении в базу данных.
Примеры:

{ "status": 500, "message": "Ошибка подключения к базе данных","id": null}
{ "status": 200, "message": null, "id": 42 }

##### При подготовке проекта использована база данных PostgreSQL, установка производится командой:

* pip install psycopg2

##### Порт, логин, пароль и путь к базе данных берется из переменных окружения с использованием библиотеки dotenv:

*  pip install python-dotenv

- FSTR_DB_HOST: путь к базе данных;
- FSTR_DB_PORT: порт базы данных;
- FSTR_DB_LOGIN: логин, с которым происходит подключение к БД;
- FSTR_DB_PASS: пароль, с которым происходит подключение к БД.
