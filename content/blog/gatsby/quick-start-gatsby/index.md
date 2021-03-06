---
title: Быстрый запуск сайта с фреймворком Gatsby
date: 2020-02-05
description: Как с помощью фреймворка Gatsby быстро развернуть сайт на локальном компьютере
---

## Создание и запуск сайта на фреймворке Gatsby

С помощью фреймворка Gatsby можно создать сайт и запустить его в локальной среде разработки всего за 5 минут. Для этого нужно выполнить четыре шага:

1. Установить Gatsby на ПК.

```
npm install -g gatsby-cli
```

2. Клонировать готовый сайт Gatsby из репозитория.

```
gatsby new my-blazing-fast-site
```

3. Запустить сайт в режиме разработки.

Для этого перейдите в корневой каталог вашего сайта и запустите его командой `develop`:

```
cd my-blazing-fast-site/
gatsby develop
```

4. Открыть исходный код и начать редактировать.

Откройте браузер и перейдите по адресу `http://localhost:8000`, где вы увидите созданый вами сайт. Откройте каталог my-blazing-fast-site в любом редакторе кода и отредактируйте `src/pages/index.js`. Сохраните изменения, и браузер автоматически обновится.

Теперь у вас есть полностью функциональный сайт на Gatsby. Дополнительную информацию о настроках сайта на Gatsby, вы можете получить на страницах [плагины](https://gatsbyjs.org/plugins/) и [учебник](https://gatsbyjs.org/tutorial/) официального сайта.

## Обучение Gatsby

Полная документация по Gatsby находится на сайте https://gatsbyjs.org/.

Для большинства разработчиков офсайт рекомендует начать с [подробного руководства по созданию сайта с помощью Gatsby](https://gatsbyjs.org/tutorial/). Руководство расчитано на то, что вы обладаете нулевым уровнем знаний и умений и знакомит со всеми шагами процесса.

Чтобы сразу погрузиться в примеры кода, обратитесь к [документации](https://gatsbyjs.org/docs/). В частности, проверьте разделы “Guides”, “API Reference” и “Advanced Tutorials” на боковой панели.

## Руководства по миграции

Если у вас уже есть сайт на фреймворке Gatsby, то эти руководства помогут вам обновить ваш сайт до Gatsby v2.

* [Миграция сайта Gatsby с v1 на v2](https://gatsbyjs.org/docs/migrating-from-v1-to-v2/)
* Ваш сайт еще на Gatsby v0? Начните отсюда: [Миграция сайта Gatsby с v0 на v1](https://gatsbyjs.org/docs/migrating-from-v0-to-v1/)



Используемые ресурсы:

* https://github.com/gatsbyjs/gatsby
