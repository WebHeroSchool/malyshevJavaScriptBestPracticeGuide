Лучшие практики JavaScript
+ Глубокая вложенность
+ Излишние комментарии
+ Избегайте крупных функций
+ Повторы кода
+ Используйте подходящие по смыслу глаголы
+ Используйте существительные для имен классов
+ В случае сомнений выбирайте описательность, а не краткость
+ Избегайте использования eval()
+ Расположение скриптов
+ Используйте PascalCase для имен классов



## Глубокая вложенность ##
Если в вашем коде много вложенных циклов или условий, возможно, что-то следует вынести в отдельную функцию.

#### Пример ####
``` js 
const exampleArray = [ [ [ 'value' ] ] ];

exampleArray.forEach((arr1) => {
  arr1.forEach((arr2) => {
    arr2.forEach((el) => {
      console.log(el)
    })
  })
})

// output: 'value'
```
В данном примере мы можем создать функцию, которая будет перебирать все массивы и возвращать итоговое значение:

#### Пример ####
``` js 
const exampleArray = [ [ [ 'value' ] ] ];

const retrieveFinalValue = (element) => {
  if(Array.isArray(element)) {
    return fetchValue(element[0]);
  }

  return element;
}

// output: 'value'
```
## Комментарии ##
Хотя использование комментариев в коде может быть полезным, это также может служить признаком того, что ваш код не является самопоясняющим.

«Несмотря на то что комментарии по сути не являются ни чем-то плохим, ни чем-то хорошим, они часто используются в качестве «костылей». Код надо писать так, будто комментарии вообще не существуют. Это будет заставлять вас писать как можно более простым и самодокументирующим способом», – Джефф Атвуд.

Код должен говорить сам за себя!

## Избегайте крупных функций ##
Крупный размер функции или даже класса намекает на то, что эта функция делает больше, чем следовало бы. Приведенный пример может показаться простым, но он хорошо иллюстрирует проблему. Эта функция делает намного больше, чем нужно.

#### Пример ####
``` js
const addMultiplySubtract = (a, b, c) => {
  const addition = a + b + c;
  const multiplication = a * b * c;
  const subtraction = a - b - c;

  return `${addition} ${multiplication} ${subtraction}`;
}
```
Будет лучше создать несколько разных функций, чтобы разделить логику:

#### Пример ####
``` js
const add = (a, b, c) => a + b + c;
const multiply = (a, b, c) => a * b * c;
const subtract = (a, b, c) => a - b - c;
```
## Повторы кода ##
Если вам приходится копировать и вставлять блок кода, это признак того, что данный блок можно выделить в отдельную функцию.
Хорошей иллюстрацией может послужить наш пример с глубокой вложенностью:

#### Пример ####
``` js
const exampleArray = [ [ [ 'value' ] ] ];

exampleArray.forEach((arr1) => {
  arr1.forEach((arr2) => {
    arr2.forEach((el) => {
      console.log(el)
    })
  })
})
```
Здесь у нас много повторяющегося кода. Будет гораздо лучше выделить его в отдельную функцию и управлять логикой иначе, с меньшим количеством повторов:

#### Пример ####
``` js
const exampleArray = [ [ [ 'value' ] ] ];

const retrieveFinalValue = (element) => {
  if(Array.isArray(element)) {
    return fetchValue(element[0]);
  }

  return element;
}
```
Другим хорошим примером повтора кода может послужить извлечение данных из параметров:

#### Пример ####
``` js
const getUserCredentials = (user) => {
  const name = user.name;
  const surname = user.surname;
  const password = user.password;
}
```
Используя деструктуризацию объекта, мы можем просто сделать следующее:

#### Пример ####
``` js
const getUserCredentials = (user) => {
  const { name, surname, password } = user;
}
```
## Используйте подходящие по смыслу глаголы ##
Функции обычно создают, читают, обновляют или удаляют (create, read, update or delete) что-либо. Можно подойти к делу даже более тщательно, чтобы ваши функции создавали, извлекали, устанавливали, добавляли, убирали, сбрасывали и удаляли (create, get, set, add, remove, reset, delete) разные вещи.

Имя функции должно быть глаголом или фразой, содержащей глагол, и должно сообщать о том, что эта функция делает.

При этом следует быть последовательным. Т.е., для извлечения данных всегда использовать get, а не get, retrieve, return и десять тысяч других слов.

В общем, должно быть:

#### Пример ####
``` js
getQuestions, getUserPosts, getUsers, 
```
а не

#### Пример ####
``` js
getQuestions, returnUsers, retrieveUsers.
```
Конечно, все это вариации одних и тех же слов, но вам нужно выбрать для себя какой-то один вариант и придерживаться его постоянно. Например, когда удаляете что-нибудь, используйте или delete, или remove (но не оба слова) во всей вашей программе.

## Используйте существительные для имен классов ##
Классы не принимают вещи, они и есть вещи. Более конкретно, они являются шаблонами чего-либо. Поэтому следует использовать

#### Пример ####
``` js
class Car = {…}
```
а не 

#### Пример ####
``` js
class MakeCar {...}.
```
## В случае сомнений выбирайте описательность, а не краткость ##
Нужно стараться быть как можно более лаконичным. Однако, если суть вашей функции двумя-тремя словами в имени не выразить, лучше описать ее большим количеством слов. 

#### Пример ####
``` js
findUserByNameOrEmail setUserLoggedInTrue //лучше, чем
findUser.
```
## Избегайте использования eval() ##
Функция eval() используется для запуска текста как кода. Практически во всех случаях нет необходимости использовать её.

Поскольку это позволяет запускать произвольный код, а также представляет проблему безопасности.

## Расположение скриптов ##
Разместите скрипты внизу страницы.

#### Пример ####
``` html 
<!DOCTYPE html>
<html>
 <head>
  <meta charset="utf-8">
  <link rel="stylesheet" href="style.css">
 </head>
 <body>
  <div class="loader" id="preloader">
    <div class="circle"></div>
    <div class="circle"></div>
    <div class="circle"></div>
  </div>
  <script type="text/javascript" src="./script.js"></script>
 </body>
</html>
```
## Используйте PascalCase для имен классов ##
Благодаря Pascal case вы сможете с легкостью отличать, что в вашем коде является классом, а что нет.

#### Пример ####
``` js 
class Task {…}
```
а не

#### Пример ####
``` js class task {...}.
```