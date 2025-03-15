# Лабораторная 1

## Отрабатываемый материал

Использование систем сборки (на выбор студента Gradle/Maven), Javadoc, JUnit

## Задание

Реализовать систему банка, настроить CI

## Сущности

- ### Юзер
  - должен иметь login, имя, возраст, пол, цвет волос (enum), список друзей
  - список друзей может меняться
- ### Счёт
  - должен иметь id, баланс, login пользователя-владельца, историю операций
  - баланс может меняться, каждое изменение баланса добавляет новый элемент в историю операций

## Функциональные требования

- создание юзера
- вывод информации о юзере
- изменение списков друзей юзеров
- создание счёта (у одного юзера может быть больше одного счёта)
- просмотр баланса счёта
- снятие денег со счёта
- пополнение счета
- перевод денег с одного счёта на другой
- за переводы между счетами снимается комиссия (между своими 0%, другу 3%, иначе 10%)

## Не функциональные требования

- При запуске сборки приложения должна автоматически генерироваться документация JavaDoc
- Интерактивный консольный интерфейс
- Данные должны быть сохранены в in-memory repository (объекты репозиториев, с коллекциями)
- Использование каких-либо ORM библиотек - запрещено
- Использование Spring Framework и Spring Boot - запрещено
- Сторонние зависимости должны поставляться системой сборки автоматически
- Решение должно быть представлено в трёх модулях

## Test cases

- снятие денег со счёта
    - при достаточном балансе проверить что сохраняется счёт с корректно обновлённым балансом
    - при недостаточном балансе сервис должен вернуть ошибку
- пополнение счёта
    - проверить что сохраняется счёт с корректно обновлённым балансом

Данные тесты должны проверять бизнес логику, они не должны как-либо зависеть от репозиториев или консольного
представления (в данных тестах необходимо использовать моки репозиториев).

# Ссылки

https://learnxinyminutes.com/docs/java/  
https://maven.apache.org/guides/getting-started/  
https://docs.gradle.org/current/userguide/part1_gradle_init.html  
https://github.com/eugenp/tutorials/blob/master/testing-modules/junit-5-basics/src/test/java/com/baeldung/ExceptionUnitTest.java

# Инстуркции по настройке CI

## Создание структуры для GitHub Actions

1. В корне репозитория создайте папку `.github/workflows`
2. В этой папке создайте файл `java.yml`

## Добавление CI скрипта

В зависимости от выбранной системы сборки, вам нужно будет вставить в этот файл различный код.

## Maven

```yaml
name: Java CI
on: [push]

jobs:
  build:
    runs-on: ubuntu-latest

    steps:
      - uses: actions/checkout@v2
      - name: Set up JDK 21
        uses: actions/setup-java@v2
        with:
          java-version: '21'
          distribution: 'temurin'
      - name: Build with Maven
        run: mvn --batch-mode --update-snapshots package
```

## Gradle

```yaml
name: Java CI
on: [push]

jobs:
  build:
    runs-on: ubuntu-latest

    steps:
      - uses: actions/checkout@v2
      - name: Set up JDK 21
        uses: actions/setup-java@v2
        with:
          java-version: '21'
          distribution: 'temurin'
      - name: Validate Gradle wrapper
        uses: gradle/actions/wrapper-validation@v3
      - name: Build with Gradle
        uses: gradle/gradle-build-action@v1
        with:
          arguments: build
```

‼️ В данных скриптах указана версия JDK 21, если вы используете другую версию, то поставьте её в параметре `java-version`
Для решения подобной проблемы  
![image](imgs/416010416-2715af2f-11fa-45c8-beca-cc28808a0024.png)
Пользователям Windows необходимо сделать дополнительную манипуляцию над gradle wrapper’ом:
```sh
git update-index --chmod=+x gradlew
```
Далее сделайте `commit`+ `push`, можно напрямую в `master` ветку, без пулл реквеста.
