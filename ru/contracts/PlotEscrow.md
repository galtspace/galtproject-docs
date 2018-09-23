# Контракт PlotEscorow

## Описание проблемы
После регистрации земельного участка Пользователь должен иметь возможность получить и принять предложение о его купле - продаже до регистрации Кастодиана, до есть до передачи прав собственности на участок Кастодиану.

## Особенности
Контракт использует функциональность PlotCustodianManager.

## Пользовательские сценарии

### Сценарий №1: Создание предложения о продаже участка.

1. Пользователь в приложении в разделе Мои участки для участка может нажать кнопку "Выставить на продажу".
2. В новом всплывающем окне он указывает: Эфиры или Контракат ERC 20 токенов в которых будет осуществлена сделка, сумма продажи, IPFS хеши фотографий и документов. Так же пользователь указывает комисси в GALT (по аналогии с другими заявками).
3. Пользователь нажимает кнопку "Подать заявку", создается транзакция с методом Создать заявку.
4. Теперь заявка видна в разделе "Маркетплейс". 

### Сценарий №2: Создание предложения о покупке Участка
1. Любой пользователь может зайти в раздел Маркетплейс и увидеть все участки, которые выставлены на текущий момент. Информация: ID, кастодиан, если есть, цена, символ токена, контракт токена (если есть), IPFS хеш. Если есть предложения, то предложения. 
2. Пользователь нажимает кнопку "Сделать предложение". Появляется поле для ввода суммы в токенах заявки.
3. Пользователь вводит суммы и нажимат "Подтвердить". Создается и отправляется транзакция.

### Сценарий №3: Принятие предложения о покупке участка.

1. Продавец рядом с каждым предложением может нажать кнопку "Ответить". Появляется окно, где он может указать свое предложение в токенах заявки.
2. Если Сумма по предложению продавца и покупателя совпадают, то статус заявки меняется на "Готова к Escrow".
3. Продавец может передать токен Space на контракт. Для этого он нажимает передать на контракт. Как только токен передан на контракт статус заявки меняется на SPACE получен(ил выставляется флаг).

### Сценарий №4: Отправка токенов для покупки участка на контракт

1. Продавец, если заявка имеет статус Готова к Escrow, может нажать кнопку перевести токены на контракт. Создаются транзакции на перевод Эфиров или ERC20 токенов для покупки.
2. После того, как токен участка и токены для покупки были переведены, то токены могут быть возвращены сторонам только Валидатором с ролью Аудитор.
3. Если токен SPACE и оплата получены контрактом, то статус - ESCROW.

### Сценарий №5: Проведение сделки
1. Сделка может быть осуществлена, если у участка назначен кастодиан.
2. Если кастодиан не назначен, то Владелец может отсюда создать заявку и назначить Кастодиана (аналогично PLotCustodianManager).
3. Если Кастодиан назначен, то Сделка осуществляется автоматически. Покупатель получает токен Участка, Продавец -  Эфиры или ERC20.
4. Стаус заявки - CLOSED.

### Сценарий №6: Возвращение токена SPACE
1. Продавец может вернуть токен SPACE до получения Контрактом токенов покупателя.
2. Для этого он нажимает кнопку "Вернуть Участок".

### Сценарий №7: Возвращение токенов Покупателю
1. Поккупатель может вернуть токены или Эфиры до получения Контрактом токена SPACE.
2. Для этого он нажимает кнопку "Вернуть оплату".

### Сценарий №8: Возвращение токенов Покупателю и Продавцу
1. Каждый участник сделки может нажать "Запросить отмену сделки".
2. Аудитор может назначить себе такую заявку.
3. После того, как она назначена он может нажать "Отменить сделку". В таком случае статус заявки меняется, токены возвращаются, комиссия не возвращается.
4. Аудитор может получить 50% от оплаченной комиссии, остальное получает GALT SPACE.

### Сценарий №9: Одобрение сделки Кастодианом
1. Если на момент подачи Завки кастодиан не был назначен, то требуется его подпись.
2. В меню он должен Нажать кнопку "Подтвердить сделку". Создается транзакция и выставляется флаг в контракте.
3. Если Кастодиан назначен, то флаг выставляется при создании заявки автоматически.