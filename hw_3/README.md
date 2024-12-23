## Домашнее задание №3

Структура данных: **Очередь Майкла-Скотта**.

Реализация структуры находится в файле `src/main/kotlin/MSQueue.kt`.

Тесты находятся в директории `src/test/kotlin`.

### Сборка без запуска тестов
```bash
gradle build -x test
```

### Сборка с запуском тестов
```bash
gradle build
```

### Запуск тестов
```bash
gradle test
```

## Описание тестов

#### Тест №1. MSQueueBasicTest

`StressTest` от Lincheck. Генерируется набор параллельных сценариев, в ходе которых исполняются методы `dequeue` и `enqueue`. Lincheck создает потоки, дожидается их готовности и одновременно запускает их на сценариях.

Ожидается, что этот тест проверяет корректность (не lock-freedom) структуры данных.

Тест исполняется порядка 10 секунд.

#### Тест №2. MSQueueObstructionFreedomTest

`checkObstructionFreedom` от Lincheck. Этот тест проверяет самую слабую форму общего прогресса системы (структуры данных) -- `obstruction-freedom`. 

> Obstruction-freedom, when any operation is completed in a bounded number of steps if all the other threads pause.

Тест исполняется порядка 40-50 секунд.

#### Тест №3. MSQueueSingleThreadTest

Несколько юнит-тестов для всех методов класса `MSQueue`. Проверка корректной работы `enqueue`, `dequeue`. Во время тестирования был выявлен баг в реализации метода `isEmpty` -- сравнивались не объекты, на которые ссылаются `AtomicReference`, а сами ссылки. Очевидно, что ссылки разные, поэтому метод всегда выдавал `false`.

#### Тест №4. MSQueueStraightforwardTest

Тест sequentialSpecification от Lincheck. Тест проверяет корректность последовательной структуры данных, в нашем случае -- очереди. Класс `SequentialQueue` -- последовательная спецификация тестируемой `MSQueue`.
Для большей сложности теста добавим `actorsBefore`, `actorsAfter` -- количество операций до и после параллельной части тестирования; `threads` -- количество потоков в параллельной части тестирования; `actorsPerThread` -- количество операций для каждого потока; `iterations` -- количество генерируемых сценариев использования структуры данных.

В файле есть два теста, каждый из которых использует свою стратегию тестирования: `StressOptions` -- генерация сценариев использования структуры, `ModelCheckingOptions` -- Bounded Model Checking.