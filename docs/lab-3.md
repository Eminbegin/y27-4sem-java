# Лабораторная работа №3

## Отрабатываемый материал

Spring Framework, Spring Boot, JpaRepository, REST API, Dependency Injection, Swagger
## Задание

К созданному в прошлых лабораторных сервису добавляется использование Spring Framework, Spring Boot, внедрения зависимостей (Dependency Injection).

Контроллеры должны предоставлять HTTP эндпоинты (**REST API**) для получения информации о конкретных пользователях и их счетах и для взаимодействия с пользователями и их счетами. 

## Функциональные требования

- Все сценарии из предыдущих лабораторных работ должны быть реализованны через HTTP эндпоинты.
- Реализовать эндпоинты для получения аккаунтов по идентификатору пользователя, получение друзей по идентификатору пользователя, получение всех пользователей системы с фильтрацией по цвету волос и гендеру, получение всех аккаунтов, получение всех операций с фильтрацией по типу и идентификатору аккаунта.

## Нефункциональные требования

- Использовать Dependency Injection
- Контроллеры не должны отдавать или принимать доменные сущности
- Репозитории должны быть Spring Bean'ами (наследоваться от JpaRepository)
- Строгое соблюдение REST спецификации для эндпоинтов
- Все эндпоинты должны иметь описание возможных кодов в Swagger документации
- Запрещается использовать xml-конфигурации для бинов (только Java-based анотации)

## Test cases

При сдаче лабораторной нужно будет показать работоспособность endpoint’ов через HTTP запросы.

Модифицировать код из предыдущих лабораторных работ разрешается
