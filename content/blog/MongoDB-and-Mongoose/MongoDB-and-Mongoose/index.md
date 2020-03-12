---
title: Основы MongoDB и Mongoose
date: 2020-01-08
description: Краткое руководство по работе с базой данных MongoDB с помощью библиотеки Mongoose
---

## Введение в MongoDB и Mongoose

**MongoDB**--база данных, которая хранит данные в виде документов для использования приложением. Как правило, документы имеют структуру, подобную JSON (JavaScript Object Notation--текстовый формат обмена данными, основанный на JavaScript). Mongo--нереляционная база данных "NoSQL". Это означает, что Mongo хранит все связанные данные в одной записи, а не хранит их во многих заранее заданных таблицах, как в базе данных SQL. Некоторые преимущества этой модели хранения заключаются в следующем:

* Масштабируемость: по умолчанию нереляционные базы данных распределяются (или "совместно используются") на множество систем, а не только на одну. Это облегчает повышение производительности при меньших затратах.
* Гибкость: новые наборы данных и свойств могут быть добавлены в документ без необходимости создавать новую таблицу для этих данных.
* Репликация: копии базы данных выполняются параллельно, поэтому, если одна из них не работает, одна из копий становится новым основным источником данных.

Хотя существует много нереляционных баз данных, использование Mongo с JSON в качестве структуры хранения документов делает его логичным выбором при изучении бэкенда JavaScript. Доступ к документам и их свойствам подобен доступу к объектам в JavaScript.

**Mongoose.js**--модуль npm для Node.js, который позволяет вам писать объекты для Mongo так же, как и в JavaScript. Это может облегчить создание документов для хранения в Mongo.

Работа над задачами в этом руководстве потребует написания кода на Glitch.

Запустите этот проект на Glitch по [этой ссылке](https://glitch.com/edit/#!/remix/clone-from-repo?REPO_URL=https://github.com/freeCodeCamp/boilerplate-mongomongoose/) или клонируйте [этот репозиторий](https://github.com/freeCodeCamp/boilerplate-mongomongoose/) на GitHub!

## Размещение бесплатного экземпляра mongodb для проектов в MongoDB Atlas 

Для решения задач в этом руководстве нужно будет сохранять кой-какие данные, для этого будет использоваться база данных MongoDB. 

Чтобы создавать веб-приложения с помощью базы данных MongoDB можно использовать три пути:

1. Для создания базы данных MongoDB и разработки приложения использовать собственный компьютер. Для этого вы должны установить [сервер Node](https://nodejs.org/ru/download/package-manager/) и [сервер базы данных MongoDB](https://docs.mongodb.com/master/installation/) на своем ПК.
2. Для создания базы данных MongoDB использовать облачный сервис MongoDB Atlas, а приложение разрабатывать и запускать на локальном ПК. Этот способ будет рассмотрен в данной статье.
3. Для создания базы данных MongoDB использовать облачный сервис MongoDB Atlas, а приложение разрабатывать и запускать на каком-нибудь облачном сервисе, например [Glitch](https://glitch.com).

Чтобы не заморачиваться с установкой и настройкой MongoDB воспользуемся облачным сервисом [MongoDB Atlas](https://www.mongodb.com/cloud/atlas), который не только упростит конфигурацию базы данных, но и позволит иметь к этой базе доступ откуда угодно и в любое время. Руководство по настройке аккаунта в MongoDB Atlas и подключению экземпляра базы данных MongoDB читайте на [этой странице]().

## Установка и настройка Mongoose и MongoDB

Дальнейшие действия предполагают, что у вас нет своего проекта, и что вы начнете с нуля.

В терминале создайте каталог `myapp` и сделайте его рабочим.

```
md myapp
cd myapp
```

С помощью команды `npm init` создайте файл `package.json`. 

```
npm init
```

Эта команда выдает целый ряд приглашений, например, приглашение указать имя и версию вашего приложения. На данный момент, достаточно просто нажать клавишу ВВОД, чтобы принять предлагаемые значения по умолчанию для большинства пунктов, кроме следующего:

```
entry point: (index.js)
```

Введите app.js или любое другое имя главного файла по своему желанию. Если вас устраивает index.js, нажмите клавишу ВВОД, чтобы принять предложенное имя файла по умолчанию.

Чтобы ваше приложение могло работать с базой данных MongoDB нужно установить драйвер. Установите драйвер MongoDB и его зависимости, выполнив в терминале из каталога `myapp` следующую команду.

```
npm install mongodb
```

Теперь установите модуль mongoose в каталоге `myapp`, набрав следующую команду в терминале.

```
npm install mongoose
```

После установки в каталоге `myapp` будут находится два файла `package.json`, `package-lock.json` и каталог `node_modules`. В файле `package.json` будут добавлены зависимости:

```json
"dependencies": {
    "mongodb": "^3.4.1",
    "mongoose": "^5.8.7"
}
```

## Переменные окружения в файле .env

Для хранения переменных окружения вы будете использовать файл `.env`. Создайте его в корне проекта и скопируйте в него URI базы данных MongoDB Atlas, полученный раннее:

```
MONGO_URI='mongodb+srv://<user>:<password>@cluster0-hsvns.mongodb.net/test?retryWrites=true&w=majority'
```

Обратите внимание: URI окружен одинарными (можно двойными) кавычками; между переменной MONGO_URI и знаком `=`, а также, между знаком `=` и URI не должно быть пробела; замените <user> на имя пользователя, а <password> на свой пароль в MongoDB Atlas. Там не должно быть символов <> (если только они не находятся в вашем пароле).

Обратите внимание, в файле `.env` хранится пароль, поэтому при сохраненинии проекта в репозиторий, данный файл нужно включить в список исключений в файле `.gitignore`.

Для того, чтобы переменные окружения из файла `env` можно было использовать в приложении нужно установить пакет `dotenv`:

```
npm install dotenv
```

В файле `package.json` будет добавлена зависимость:

```json
  "dependencies": {
    "dotenv": "^8.2.0", 
  }
```

Теперь, если вам необходимо использовать какую-нибудь переменную окружения из файла `env` в одном из файлов вашего приложения, вы должны в этом файле просто подключить пакет `dotenv` следующим образом:

```js
require('dotenv').config();
```

Теперь все переменные из файла `.env` будут доступны в `process.env`. Чтобы прочитать значение переменной, например, PASSWORD нужно обратиться к свойству `process.env.PASSWORD`.

## Подключение БД MongoDB

В корне проекта создайте файл `index.js`, в который скопируйте следующий код.

```js 
//Подключение к файлу модуля mongoose под именем mongoose
var mongoose = require('mongoose');

//Использование пакета dotenv для чтения переменных из файла .env в Node
require('dotenv').config();

//Соединение с базой данных
mongoose.connect(process.env.MONGO_URI, { useNewUrlParser: true, useUnifiedTopology: true }, function (err) {
  //Если при соединении с БД происходит ошибка, то выбрасывается исключение, и все дальнейшее исполнение функции прерывается.
  if (err) throw err;
  //Если соединение с БД выполнено успешно выводится сообщение 'БД подключена'
  console.log('БД подключена');
});
```
В функции `connect()` первый параметр `process.env.MONGO_URI` - это URI для подключения приложения к БД (в данном случае значение свойства MONGO_URI хранится в файле `.env`). Вторым параметром в функции `connect()` является необязательный объект опций. Третий параметр - это функция обратного вызова, которая будет вызвана после попытки соединения с базой данных.

## Создание модели

### CRUD Часть I - создание

CRUD - это сокращение для операций Create, Read, Update and Delete (создать, прочесть, обновить и удалить). Эти операции являются основными для работы с базами данных, таких как MongoDB.

В mongoose все завязано на 2х ключевых понятиях Схема(Schema) – описание сущности и Модель – сама сущность.

Прежде всего вам нужна [схема]https://mongoosejs.com/docs/guide.html. 

Создадайте схему и модель из неё.

В файл `index.js` скопируйте следующий код.

```js
require('dotenv').config();
const mongoose = require('mongoose');

mongoose.connect(process.env.MONGO_URI, { useNewUrlParser: true, useUnifiedTopology: true }, function (err) {
  if (err) throw err;
  console.log('БД подключена');
});

//Создание схемы
var userSchema = new mongoose.Schema({
  name: { type: String, default: "Анонимный" },
  age: { type: Number, min: 18, index: true }
});

//Создание модели из схемы.
const UserModel = mongoose.model("UserModel", userSchema);
```

Каждое поле в `mongoose.Schema` характеризуется типом и может иметь дополнительные характеристики: `default`, `min` и `max` (для Number), `match` и `enum` (для String), `index` и `unique` (для индексов). Подробнее о типах можно почитать [тут](https://mongoosejs.com/docs/schematypes.html).

В функции `mongoose.model` первый параметр - это имя модели, второй параметр - имя схемы, из которой создается модель.

Схемы - это строительный блок для моделей. Модель позволяет создавать экземпляры ваших объектов, называемых документами.

## Создание и сохранение записи модели

В файле `index.js` замените содержимое на следующий код.

```js
require('dotenv').config();
const mongoose = require('mongoose');

mongoose.connect(process.env.MONGO_URI, { useNewUrlParser: true, useUnifiedTopology: true }, function (err) {
  if (err) throw err;
  console.log('БД подключена');
});

var userSchema = new mongoose.Schema({  
  name: { type: String, default: "Анонимный" },
  age: { type: Number, min: 18, index: true },
  favoriteFoods: [String]
});

const UserModel = mongoose.model("UserModel", userSchema);

//Создание объекта модели, т. е. документа
var ivanPetrov = new UserModel({ name: "Ivan Petrov", age: 25, favoriteFoods: ["чипсы", "кока-кола"] });

//Сохранение документа в БД
ivanPetrov.save(function (err, data) {
  if (err) return console.error(err);
  console.log('Пользователь с именем ' + data.name + ' сохранен');
});
```

Метод `save()` должен сохранить документ в базе данных mongodb. Если сохранение прошло успешно, будет выведено на консоль 'Пользователь с именем Ivan Petrov сохранен', если же произошла ошибка, то будет выведено соответствующее сообщение об ошибке.

В вашей базе данных теперь должен быть один документ с именем "Ivan Petrov". 

## Создание нескольких записей с помощью model.create()

Выше было показано, как сохранить документ в базе данных mongodb с помощью метода mongoose `save()`. Но что если нужно сохранить много документов, например, из массива. Для этого можно применить другой метод mongoose - `create()`.

В файле `index.js` замените содержимое на следующий код.

```js
require('dotenv').config();
const mongoose = require('mongoose');

mongoose.connect(process.env.MONGO_URI, { useNewUrlParser: true, useUnifiedTopology: true }, function (err) {
  if (err) throw err;
  console.log('БД подключена');
});

var userSchema = new mongoose.Schema({  
  name: { type: String, default: "Анонимный" },
  age: { type: Number, min: 18, index: true },
  favoriteFoods: [String]
});

const UserModel = mongoose.model("UserModel", userSchema);

//Массив, из которого данные будут помещены в БД
var arrayUsers = [
  { name: "Светлана", age: 21, favoriteFoods: ["чипсы", "кофе"] },
  { name: "Kamila", age: 35, favoriteFoods: ["гамбургер", "кока-кола"] },
  { name: "Олег", age: 27, favoriteFoods: ["роллы", "кофе"] }
];

UserModel.create(arrayUsers, function (err, users) {
  if (err) return console.log(err);
  console.log('В базе данных созданы ' + users.length + ' документа');
});

```

Таким образом с помощью функции `create()` из массива `arrayUsers` были добавлены еще три документа в БД, а на консоль выведена сообщение "В базе данных созданы 3 документа". Обратите внимание, в базе данных теперь четыре документа.

Первый аргумент в методе `Model.create()` - это документы в виде массива или объекта, которые будут вставлены в БД. Второй аргумент - это функция обратного вызова.

В функции обратного вызова в первый аргумент `err` передается ошибка, а во второй аргумент `users` передаётся массив `arrayUsers`.

## Использование model.find() для поиска в базе данных

В файл `index.js` скопируйте следующий код.

```js
require('dotenv').config();
const mongoose = require('mongoose');

mongoose.connect(process.env.MONGO_URI, { useNewUrlParser: true, useUnifiedTopology: true }, function (err) {
  if (err) throw err;
  console.log('БД подключена');
});

var userSchema = new mongoose.Schema({
  name: { type: String, default: "Анонимный" },
  age: { type: Number, min: 18, index: true }
});

const UserModel = mongoose.model("UserModel", userSchema);

var userName = "Светлана";

//Поиск в БД
UserModel.find({ name: userName }, function (err, data) {
  if (err) return console.log(err);
  console.log('Все пользователи с именем ' + userName + ' найдены. Их всего ' + data.length);
});
```

Первый параметр в функции `find()` - это селектор, являющийся объектом, который указывает, что нужно искать в базе данных. Если селектор не указан, возвращаются все документы из БД. Вторым параметром в функции `find()` является функция обратного вызова.

Функция `find()` находит и возвращает все документы, соответствующие селектору. Результатом будет массив документов.

Если в результате будет слишком много документов, чтобы поместиться в памяти, используйте функцию `cursor()`


## Использование model.findOne() для возвращения одного документа из базы данных

В mongoose есть метод `findOne()`, который ведет себя как метод `find()`, но возвращает только один документ (не массив). Даже если документов с данным параметром поиска несколько метод `findOne()` возвращает первый найденный документ. Это особенно полезно при поиске по свойствам, которые вы объявили уникальными.

В файл `index.js` скопируйте следующий код.

```js
require('dotenv').config();
const mongoose = require('mongoose');

mongoose.connect(process.env.MONGO_URI, { useNewUrlParser: true, useUnifiedTopology: true }, function (err) {
  if (err) throw err;
  console.log('БД подключена');
});

var userSchema = new mongoose.Schema({  
  name: { type: String, default: "Анонимный" },
  age: { type: Number, min: 18, index: true },
  favoriteFoods: [String]
});

const UserModel = mongoose.model("UserModel", userSchema);

UserModel.findOne({ name: "Светлана" }, function (err, data) {
  if (err) return console.log(err);
  console.log('Пользователь ' + data.name + ' найден');
});
```

Метод `findOne()` находит в базе данных первый попавшийся документ со свойством `{ name: "Светлана" }` и возвращает его. Если в качестве первого параметра в функции `findOne()` ничего не указано, mongoose вернет произвольный документ.

## Использование model.findById() для поиска в базе данных по id

Когда в базу данных сохраняется документ, mongodb автоматически добавляет поле `_id` и присваивает ему уникальный буквенно-цифровой ключ. Поиск по `_id` является очень частой операцией, поэтому mongoose предоставляет специальный метод для этого - `findById()`.

В файл `index.js` скопируйте следующий код.

```js
require('dotenv').config();
const mongoose = require('mongoose');

mongoose.connect(process.env.MONGO_URI, { useNewUrlParser: true, useUnifiedTopology: true }, function (err) {
  if (err) throw err;
  console.log('БД подключена');
});

var userSchema = new mongoose.Schema({  
  name: { type: String, default: "Анонимный" },
  age: { type: Number, min: 18, index: true },
  favoriteFoods: [String]
});

const UserModel = mongoose.model("UserModel", userSchema);

//Определенине id для поиска
var userId = "5e24c27a0d07d02119c39ed7";

//Поиск документа по _id
UserModel.findById(userId, function (err, data) {
  if (err) return console.log(err);
  console.log('Пользователь c id = ' + data._id + ' найден, его зовут ' + data.name + ', ему ' + data.age + ' лет');
});
```
Если документ с указанным id найден, то на консоль будет выведено сообщение "Пользователь c id = 5e24c27a0d07d02119c39ed7 найден, его зовут Олег, ему 27 лет".

## Обновление документов в БД с помощью стандартного поиска, присвоения и сохранения

Для того, чтобы изменить (обновить) документ в базе данных, в mongoose существуют методы `update`, `findByIdAndUpdate` и `findOneAndUpdate`. Но сначала нелишнем будет узнать о классическом способе изменения документов. Этот способ состоит из уже изученных вами методов, а именно: `findOne`, `findById` и `save`.

В файл `index.js` скопируйте следующий код.

```js
require('dotenv').config();
const mongoose = require('mongoose');

mongoose.connect(process.env.MONGO_URI, { useNewUrlParser: true, useUnifiedTopology: true }, function (err) {
  if (err) throw err;
  console.log('БД подключена');
});

var userSchema = new mongoose.Schema({
  name: { type: String, default: "Анонимный" },
  age: { type: Number, min: 18, index: true },
  favoriteFoods: [String]
});

const UserModel = mongoose.model("UserModel", userSchema);

/*Обновление документа*/
//Поиск документа по _id 
UserModel.findById("5e25a8e88170fb0f8ce90f6f", function (err, user) {
  if (err) return console.error(err);

  //Присвоение измененных значений 
  user.name = 'Светлана Иванова';
  user.favoriteFoods.push("гамбургер")

  //Сохранение документа в БД
  user.save(function (err) {
    if (err) throw err;
    console.log('Информация о пользователе ' + user.name + ' обновлена');
  });
});
```

## Обновление документов в БД с помощью model.findOneAndUpdate()

В последних версиях mongoose есть методы, упрощающие обновление документов. Но некоторые более продвинутые функции (например, хуки pre/post, валидация) ведут себя по-другому при этом подходе, поэтому классический метод все еще полезен во многих ситуациях. 

В файл `index.js` скопируйте следующий код.

```js
require('dotenv').config();
const mongoose = require('mongoose');

mongoose.connect(process.env.MONGO_URI, { useNewUrlParser: true, useUnifiedTopology: true }, function (err) {
  if (err) throw err;
  console.log('БД подключена');
});

var userSchema = new mongoose.Schema({
  name: { type: String, default: "Анонимный" },
  age: { type: Number, min: 18, index: true },
  favoriteFoods: [String]
});

const UserModel = mongoose.model("UserModel", userSchema);

//Обновление документа в БД
UserModel.findOneAndUpdate(
  { name: 'Олег' },
  { name: 'Олег Сидоров', age: 28 },
  { new: true },
  function (err, user) {
    if (err) return console.error(err);
    console.log('Информация о пользователе ' + user.name + ' обновлена');
  }
);
```

Функция `findOneAndUpdate()` находит пользователя по условию, указанному в первом параметре `{ name: 'Олег' }`, затем устанавливает свойства, указанные во втором параметре `{ name: 'Олег Сидоров', age: 28 }`. Третий параметр `{ new: true }` в функции `findOneAndUpdate()` указывает на то, чтобы функция возвращала измененный документ, а не оригинал. Т. е. при при `new` установленном в `true` на консоле будет выведено `'Информация о пользователе Олег Сидоров обновлена'`, а при `new` установленном в `false` на консоле будет выведено `'Информация о пользователе Олег обновлена'`. По умолчанию `new` установлено в `false`. Четвертый параметр в функции `findOneAndUpdate()` - это функция обратного вызова.

## Удаление документов из MongoDB с помощью Mongoose

Для того, чтобы удалить документы из БД MongoDB в Mongoose существуют методы 
`remove()`, `deleteMany()`, `deleteOne()`, `findOneAndDelete()`, `findByIdAndRemove()` и `findOneAndRemove()`. 

### Удаление одного документа с помощью model.findByIdAndRemove

В файл `index.js` скопируйте следующий код.

```js
require('dotenv').config();
const mongoose = require('mongoose');

mongoose.connect(process.env.MONGO_URI, { useNewUrlParser: true, useUnifiedTopology: true }, function (err) {
  if (err) throw err;
  console.log('БД подключена');
});

var userSchema = new mongoose.Schema({
  name: { type: String, default: "Анонимный" },
  age: { type: Number, min: 18, index: true },
  favoriteFoods: [String]
});

const UserModel = mongoose.model("UserModel", userSchema);

UserModel.findByIdAndRemove("5e25a8e88170fb0f8ce90f71", function (err, user) {
  if (err) return console.error(err);
  console.log('Пользователь ' + user.name + ' удален из БД');
});
```

Метод `findByIdAndRemove()` находит документ по `Id`, заданному в первом параметре, и удаляяет этот документ. Если документ найден, то он возвращается в функцию обратного вызова (в данном случае, в параметр `user`). Первый параметр `Id` может быть определен как строка `"5e25a8e88170fb0f8ce90f71"`, номер `345924` или объект `{ _id: "5e25a8e88170fb0f8ce90f71" }`.

### Удаление нескольких документов с помощью model.remove()

Функция `Model.remove()` полезна для удаления всех документов, соответствующих заданным критериям.

```js
require('dotenv').config();
const mongoose = require('mongoose');

mongoose.connect(process.env.MONGO_URI, { useNewUrlParser: true, useUnifiedTopology: true }, function (err) {
  if (err) throw err;
  console.log('БД подключена');
});

var userSchema = new mongoose.Schema({
  name: { type: String, default: "Анонимный" },
  age: { type: Number, min: 18, index: true },
  favoriteFoods: [String]
});

const UserModel = mongoose.model("UserModel", userSchema);

UserModel.remove({ name: "Tom" }, function (err, data) {
  if (err) return console.log(err); 
    console.log('Удалено ' + data.n + ' документов из БД');    
})
```

Примечание: Метод `remove()` возвращает не удаленный документ, а объект JSON, содержащий результат операции и количество удаленных элементов. 

## Цепочка помощников по поисковым запросам для сужения результатов поиска

Если вы не передадите функцию обратнного вызова в качестве последнего аргумента в методе `Model.find()` (или в других методах поиска), то запрос не будет выполнен. Запрос можно сохранить в переменной для последующего использования. Этот тип объектов позволяет построить запрос с использованием цепочечного синтаксиса. Фактический поиск в БД выполняется, когда вы окончательно прицепите метод `.exec()`. Вы всегда должны передавать свою функцию обратного вызова этому последнему методу. Есть много помощников запроса, здесь вы узнаете о самых "известных" из них.

```js
require('dotenv').config();
const mongoose = require('mongoose');

mongoose.connect(process.env.MONGO_URI, { useNewUrlParser: true, useUnifiedTopology: true }, function (err) {
  if (err) throw err;
  console.log('БД подключена');
});

var userSchema = new mongoose.Schema({
  name: { type: String, default: "Анонимный" },
  age: { type: Number, min: 18, index: true },
  favoriteFoods: [String]
});

const UserModel = mongoose.model("UserModel", userSchema);

UserModel.find({ favoriteFoods: 'чипсы' })
  .sort({ name: 'asc' })
  .limit(2)
  .select('-age')
  .exec(function (err, user) {
    if (err) return console.error(err);
    console.log('Найдены пользователи, которые любят чипсы');
    console.log(user);
  });  
```

Вышеприведенный код находит в базе данных людей, которые любят `чипсы`, сортирует их по имени, ограничивает результаты поиска двумя документами и при выводе результатов скрывает их возраст. Результат выводится в виде массива документов.

`sort({ name: 'asc' })` - Устанавливает порядок сортировки по полю `name`. Допустимые значения для сортировки: `asc`, `ascending` или `1` - сортировка по возрастанию; `desc`, `descending` или `-1` - сортировка по убыванию. В качестве параметра сортировки можно задавать не только объект, но и строку. В этом случае должен быть разделенный пробелом список имен полей. Если перед именем поля не стоит знак "минус", то порядок сортировки будет возрастающим, если знак "минус" стоит, то порядок сортировки будет убывающим.

`limit(2)` - Ограничивает максимальное количество документов, возвращаемых в запросе, - двумя.

`select('-age')` - Указывает, что поле `age` (указывающее возраст) должно быть исключено из выводимого результата. На это указывает знак "минус" перед именем поля. 

`exec(callback)` - Выполняет запрос.

Более подробно о помощниках запросов смотри [здесь](https://mongoosejs.com/docs/api/query.html)

**Используемые ресурсы:**

- https://www.freecodecamp.org/learn/apis-and-microservices/mongodb-and-mongoose/

* https://mongoosejs.com/

* https://code.tutsplus.com/ru/articles/an-introduction-to-mongoose-for-mongodb-and-nodejs--cms-29527

* http://stepansuvorov.com/blog/2012/11/mongoose-%D0%B4%D0%BB%D1%8F-mongodb/

* https://developer.mozilla.org/ru/docs/Learn/Server-side/Express_Nodejs/mongoose

* https://metanit.com/nosql/mongodb/

* http://www.coldfox.ru/article/5be022d49227d914a1c83fe3/%D0%9F%D0%BE%D0%B4%D1%80%D0%BE%D0%B1%D0%BD%D0%BE%D0%B5-%D1%80%D1%83%D0%BA%D0%BE%D0%B2%D0%BE%D0%B4%D1%81%D1%82%D0%B2%D0%BE-%D0%BF%D0%BE-MongoDB-Mongoose