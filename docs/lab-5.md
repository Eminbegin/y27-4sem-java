# Лабораторная работа 5

## Отрабатываемый материал 

Асинхронное межсервисное взаимодействие, Kafka/RabbitMQ

## Задание

Реализовать отдельное Spring Boot (Storage) приложение для хранения событий о создании и изменении сущностей пользователей и счетов. Bank-service должен отправлять события в соответствующие топики:  
- Для пользователей `client-topic`  
- Для счетов `account-topic`  

Ключом сообщения должен быть идентификатор сущности (пользователя/счета), а значением - JSON с информацией об изменении.  

## Функциональные требования

- Bank-service должен начать публиковать события в топики связанных сущностей
- Storage должен сохранять события из топиков `client-topic` и `account-topic` в свою базу данных (в разных таблицах)

## Нефункциональные требования

- Запрещается использование каких-либо других брокеров сообщений кроме Kafka и RabbitMQ 
- Gateway никак не должен быть связан с Storage

### Примечание
Сервис из первых трёх лабораторных работы - Bank-service

Сервис из четвертой лабораторной работы - Gateway

Сервис из пятой лабораторной работы - Storage
