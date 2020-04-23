---
title: Качество кода и тестирование с помощью Chai
description: 
date: 2020-04-22
---

Для написания статьи использованы источники: [chaijs](https://www.chaijs.com/guide/) и [freecodecamp](https://www.freecodecamp.org/learn/information-security-and-quality-assurance/quality-assurance-and-testing-with-chai/).

Chai – библиотека, предоставляющая различные функции для проверки утверждений. Chai - это библиотека утверждений BDD/TDD для node и браузера, которая может быть великолепно сопряжена с любой платформой тестирования javascript.

Чай имеет несколько интерфейсов, которые позволяют разработчику выбрать наиболее удобный. Цепочечные стили BDD обеспечивают выразительный язык и читаемый стиль, в то время как стиль TDD assert обеспечивает более классическое ощущение.

Пакет доступен через npm:

```
npm install chai
```

## Введение в обеспечение качества с цепными проблемами

Поскольку ваши программы становятся все более сложными, вам нужно часто тестировать их, чтобы убедиться, что любой новый код, который вы добавляете, не нарушает первоначальную функциональность программы. Chai - это библиотека тестирования JavaScript, которая помогает вам проверить, что ваша программа все еще ведет себя так, как вы ожидаете, после внесения изменений. Используя Chai, вы можете написать тесты, описывающие требования вашей программы, и посмотреть, соответствует ли она им.

## Узнайте, как работают утверждения JavaScript

Используйте assert.isNull () или assert.isNotNull (), чтобы заставить тесты пройти.

## Проверьте, определена ли переменная или функция

Используйте assert.isDefined () или assert.isUndefined (), чтобы заставить тесты пройти.
