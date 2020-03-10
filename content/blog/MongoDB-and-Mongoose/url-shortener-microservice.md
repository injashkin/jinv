---
title: Генерация коротких URL адресов
description: Микросервис сокращает URL адреса, а при вводе коротких URL преобразует обратно в исходные. Написано на JavaScript
date: 2020-03-01
---

Данная статья описывает мой учебный проект на [FreeCodeCamp](https://www.freecodecamp.org/learn/apis-and-microservices/apis-and-microservices-projects/url-shortener-microservice).

Чтобы понять, для чего нужен этот микросервис прочтите статью [Сокращение URL](https://ru.wikipedia.org/wiki/%D0%A1%D0%BE%D0%BA%D1%80%D0%B0%D1%89%D0%B5%D0%BD%D0%B8%D0%B5_URL) на Википедии, а также прочтите [эту статью](https://www.internet-technologies.ru/articles/rukovodstvo-po-sokrascheniyu-url-adresov-i-otslezhivaniyu-socsetey.html).

## Задание

Нужно создать JavaScript приложение полного цикла, которое функционально похоже на это: https://thread-paper.glitch.me/.

Работа над этим проектом будет включать в себя написание кода на Glitch. Чтобы приступить к написанию кода запустите проект по [этой ссылке](https://glitch.com/edit/#!/remix/clone-from-repo?REPO_URL=https://github.com/freeCodeCamp/boilerplate-project-urlshortener/) или клонируйте [этот репозиторий](https://github.com/freeCodeCamp/boilerplate-project-urlshortener/) с GitHub!

1. Можно отправить URL-адрес в [project_url]/api/shorturl/new, и получить ответ в виде сокращенного URL-адреса в формате JSON, например: `{"original_url":"www.google.com", "short_url": 1}`
2. Если передать недопустимый URL-адрес, который не соответствует формату http(s)://www.example.com(/more/routes), то ответ в JSON будет содержать ошибку: `{"error":"invalid URL"}`. Подсказка: чтобы убедиться, что отправленный url-адрес указывает на допустимый сайт, можно использовать функцию `dns.lookup(host, cb)` от модуля ядра `dns`.
3. Когда посещается сокращенный URL-адрес, происходит перенаправление на оригинальную ссылку.

Пример Создания:
POST [project_url]/api/shorturl/new - body (urlencoded) : url=https://www.google.com

Использование:
[this_project_url]/api/shorturl/3

Вы будете перенаправлены на:
https://www.freecodecamp.org/forum/

После завершения этого проекта нужно скопировать публичный url главной страницы приложения Glitch на [эту страницу](https://www.freecodecamp.org/learn/apis-and-microservices/apis-and-microservices-projects/url-shortener-microservice). По желанию можно написать свой проект на другой платформе, но он должен быть публично виден для тестирования.

## Решение

