# Домашнее задание

Работать над игровым лаунчером предстоит в файле `/AppModules/launcher/index.js`. После выполнения всех шагов потребуется запустить лаунчер в основном исполняемом файле `/index.js`. Если объяснений в инструкции будет мало, заглядывай в урок «Дэзэшечка» в теме «Основы NodeJS и Express». Удачи!

## Шаг #1. Импорт модулей

Подключи встроенный модуль `readline` и создайте интерфейс с базовыми опциями: `input, output, terminal, prompt`;

Подключи модуль `dictionary` — это словарь со всеми сообщениями для пользователя;

Подключи модуль `games` — это объект со всеми играми.

## Шаг #2. Массив для игр `gamesArray`

Создай массив `gamesArray`, представляющий доступные игры из объекта `games` и соответствующие им идентификаторы. Для каждой игры в массиве содержится объект. Каждый объект имеет следующую структуру:

- `id` — уникальный идентификатор игры строкового типа;
- `game` — функция-игра из объекта `games`.

В массиве 6 объектов, где каждый идентификатор соответствует своей игре:

- `"1"` — knightDragonAndPrincessGame;
- `"2"` — poleChudesGame;
- `"3"` — makeWordGame;
- `"4"` — blackJackGame;
- `"5"` — trueOrFalseGame;
- `"6"` — dropCoin.

## Шаг #3. Функция `startGame`

Создай асинхронную функцию, которая принимает параметр `gameId`, ищет соответствующую игру в массиве `gamesArray` и запускает её. Параметр `gameId` — это строка, содержащая идентификатор игры. Она передаётся в функцию `startGame`, чтобы определить, какую игру нужно запустить.

Сначала функция использует метод `find` для поиска игры в массиве, сравнивая идентификатор, указанный в объекте игры, с параметром `gameId`.

Затем функция проверяет результат работы метода `find`. Если игра с таким идентификатором найдена в массиве, она запускается вызовом функции `game()`. Обрати внимание, что для подсчёта результатов только после завершения игры необходимо указать ключевое слово `await` функции запуска игры.

Подсчёт результатов осуществляется вызовом функции `countResult`. Функция запуска игры после завершения возвращает результат, который передаётся функции `countResult` в качестве аргумента. После чего вызывается функция `afterGame` с параметром `gameId` в качестве аргумента. Логика работы последних двух функций описана ниже.

Проверка на этом не заканчивается, и, если `gameId` не равен ни одному идентификатору игры, в консоль выводится сообщение из словаря с ключем `dictionary.global.wrongInput`. Затем вызывается функция `startLauncher`. Логика работы функции `startLauncher` описана ниже.

## Шаг #4. Функция `countResult`

Создай функцию, которая принимает результат игры в качестве параметра `gameResult`. Результат игры может иметь значение `true`, если победа, `false`, если поражение, или строковое значение `"draw"`, если победила дружба (ничья). Функция проверяет результат игры, выводя в консоль нужное сообщение:

- Если результат игры равен `"draw"`, функция выводит фразу по ключу `dictionary.global.draw`;
- Иначе, осуществляется проверка тернарным оператором на значение `true` или `false`. Для значения `true` функция выводит фразу по ключу `dictionary.global.win`. Для значения `false` функция выводит фразу по ключу `dictionary.global.lose`.

## Шаг #5. Функция `afterGame`

Создай функцию, которая принимает идентификатор игры в качестве параметра `gameToRepeatId`. Эта функция запускается после завершения и вывода результата определённой игры и спрашивает пользователя, что делать дальше. Функция предлагает сыграть в эту же игру ещё раз, выбрать другую игру или выйти из программы:

- Если пользователь вводит `1`, вызвается функция `startGame` с `gameToRepeatId` в качестве аргумента;
- Если пользователь вводит `2`, вызвается функция `startLauncher`;
- Если пользователь вводит `3`, вызвается функция `stopLauncher`.

## Шаг #6. Функция `startLauncher`

Создай функцию `startLauncher`, которая вызывает метод `readline.question` и спрашивает пользователя, в какую игру он хочет сыграть. Вопрос можно получить из словаря с ключом `dictionary.global.chooseGame`.

После этого происходит проверка ответа пользователя. Если пользователь ввёл число `7`, запускается функция `stopLauncher`, логика работы которой описана ниже. Иначе вызывается функция `startGame` с ответом пользователя в качестве аргумента. Эта функция будет вызываться в самом начале программы, её нужно экспортировать из модуля, используя переменные `module` и `exports`. Обрати внимание, что она также будет вызываться после каждой игры, если пользователь захочет выбрать другую игру (в функции `afterGame`).

## Шаг #7. Функция `stopLauncher`

Создай функцию `stopLauncher`, которая выводит в консоль прощальную фразу из словаря по ключу `dictionary.global.goodbye`. После чего функция прекращает работу `readline`, используя метод `close()`.

## Шаг #8. Запуск лаунчера

В главном файле приложения вызови функцию `startLauncher`. Для этого перейди в файл `/index.js`, импортируй функцию и вызовите её из текущего модуля.

Проверить работу лаунчера можно командой `node index.js`.
