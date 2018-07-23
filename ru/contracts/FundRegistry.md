# FundRegistry
Глобальный контракт учета реестров


## Разделы

* [Описание проблемы](#Описание-проблемы)
* [Цели контракта](#Цели-контракта)
* [Спецификация](#Спецификация)
* [Проблемы](#Проблемы)

## Описание проблемы
* Нужен интерфейс для создания нового фонда
* Фондам нужен интерфейс взаимодействия между собой

## Цели контракта
* Вести учет фондов
* Вести реестр создателей фондов
* Предоставить интерфейс для создания нового фонда
* Предоставить локальным контрактам фондов возможность обращаться к локальным контрактам других фондов

## Спецификация
* Контракт не изменяем
* Контракт не принадлежит ни одному пользователю

### Реестр Фондов
* Контракт реестра фондов предоставляет метод для создания нового фонда, который может вызвать
любой желающий.
* Стоимость создания нового фонда фиксирована и не изменяема: 500 000 GALT, средства перечисляются
на мультисиг фонда #0

## Проблемы
* Рассмотреть возможность использования vickrey аукциона для создания нового фонда https://github.com/andromedaspace/galtproject-docs/issues/45
* Необходимо изучить вопрос выделения определенного функционала в отдельный обновляемый контракт.