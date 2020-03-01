---
title: Сокращатель URL на JavaScript
---

## Микросервис, сокращающий URL

Данная статья является моим учебным проектом на сайте [FreeCodeCamp](https://www.freecodecamp.org/learn/apis-and-microservices/apis-and-microservices-projects/url-shortener-microservice).

Задание: 

Нужно создать JavaScript приложение полного цикла, которое функционально похоже на это: https://thread-paper.glitch.me/.

Работа над этим проектом будет включать в себя написание кода на Glitch. После завершения этого проекта нужно скопировать свой публичный url Glitch (главную страницу вашего приложения) на [этот экран](https://www.freecodecamp.org/learn/apis-and-microservices/apis-and-microservices-projects/url-shortener-microservice), чтобы протестировать его! По желанию можyj написать свой проект на другой платформе, но он должен быть публично виден для тестирования.

Запустите этот проект на Glitch по [этой ссылке](https://glitch.com/edit/#!/remix/clone-from-repo?REPO_URL=https://github.com/freeCodeCamp/boilerplate-project-urlshortener/) или клонируйте [этот репозиторий](https://github.com/freeCodeCamp/boilerplate-project-urlshortener/) на GitHub! Если вы используете Glitch, не забудьте сохранить ссылку на ваш проект в безопасном месте!

1. Можно отправить URL-адрес в [project_url]/api/shorturl/new, и получить ответ в виде сокращенного URL-адреса в формате JSON, например: `{"original_url":"www.google.com", "short_url": 1}`
2. Если передать недопустимый URL-адрес, который не соответствует формату http(s)://www.example.com(/more/routes), то ответ JSON будет содержать ошибку: `{"error":"invalid URL"}`. Подсказка: чтобы убедиться, что отправленный url-адрес указывает на допустимый сайт, можно использовать функцию `dns.lookup(host, cb)` от модуля ядра `dns`.
3. Когда посещается сокращенный URL, происходит перенаправление на оригинальную ссылку.

Пример Создания:
POST [project_url]/api/shorturl/new - body (urlencoded) : url=https://www.google.com

Использование:
[this_project_url]/api/shorturl/3

Вы будете перенаправлены на:
https://www.freecodecamp.org/forum/