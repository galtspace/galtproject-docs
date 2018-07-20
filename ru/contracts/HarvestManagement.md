# Управление урожаями / Harvest Management
## Описание проблемы
Необходимо создать систему учета для сельскохозяйственной продукции, которая бы позволила по уникальному идентификатору упаковки конечного продукта, например вина, проследить весь путь от конкретного участка земли до бутылки. 
## Цели контракта
- для каждого участка землю, определенного геохешем учитывать урожай плодов в килограммах или штуках;
- сделать так, чтобы данные нельзя было подделать при помощи криптографии;
- сделать возможность контроля и учета потерь продукции на всем пути от сбора урожая до полки;

## Общие положения
В системе для основной единицы учета принять участок земли. Каждый участок земли адресовать геохешем и на каждый участок земли выпускать токен стандарта ERC721. Каждый участок земли определенного размера будет создавать урожай, который будет учитываться в килограммах. Каждый урожай с каждого участка будет учитываться, как уникальная партия продукции. 

Цепочку блоков нужно использовать свою на базе Эфира. Можно использовать 7-8 нод, которые будут валидировать транзакции и обеспечивать достоверность всех записываемых данных. Производительность 1000 транзакций в секунду.


## Пользовательский сценарий

### Сценарий №1 Учет производства вина.
1. Пользователь - сборщик урожая собирает виноград в Cinqua Terra. Пользователь имеет свой уникальный адрес 0x4FDE31E09266423d5f1B8bf16dC8DeF085C197E5, и приватный ключ, которым он может подписывать транзакции.

2. Существует токен стандарта ERC721, который соответствует участку с виноградником. Этот участок адресуется геохешем [spyfvqwnd](https://explorer.galtproject.io/map/#spyfvqwnd). Размер участка 4.77 х 4.77 метра.

3. Пользователь - сборщик урожая 0x4FDE31E09266423d5f1B8bf16dC8DeF085C197E5 собрал 30 кг винограда с участка. Пользователь кладет коробку на Умные весы. Вводит геохеш участка и свой адрес, создает транзакцию на упаковку винограда и подписывает транзакцию своим закрытым ключом. Весы тоже имеют свой адрес 0x4FED1fC4144c223aE3C1553be203cDFcbD38C581 и закрытый ключ. Весы взвешивают виноград, создают и подписывают транзакцию по результатам взвешивания. Весы печатают этикетку с штрихкодом 1E09266423d5f1B8b.

Происходит запись данных в блокчейн. Фактически записывается, что Сотрудник 0x4FDE31E09266423d5f1B8bf16dC8DeF085C197E5 собрал и упаковал 30 кг винограда:

|id участка|Идентификатор упаковки|Количество|Сотрудник/Робот|
|----------|----------|----------|----------|
|spyfvqwnd|1E09266423d5f1B8b|30|0x4FDE31E09266423d5f1B8bf16dC8DeF085C197E5|

Эти данные нельзя подделать и изменить.

4. Весы печатают этикетку с штрихкодом 1E09266423d5f1B8b. и сборщик наклеивает его на коробку.

5. Пользователь передает коробку водителю. При передаче коробки Сборщик указывает адрес водителя 0xf3101865bd9dbe720464e684247a13269cca70660xf, указывает идентификатор коробки, создает и подписывает транзакцию на передачу коробки. Водитель тоже создает и подписывает транзакцию на получение коробки.

В блокчейне происходят следующие изменения данных:

|id участка|Идентификатор упаковки|Количество|Сотрудник/Робот|
|----------|----------|----------|----------|
|spyfvqwnd|1E09266423d5f1B8b|0|0x4FDE31E09266423d5f1B8bf16dC8DeF085C197E5|
|spyfvqwnd|1E09266423d5f1B8b|30|0xf3101865bd9dbe720464e684247a13269cca70660xf|

Фактически 30 кг винограда перешло от Сборщика к Водителю.

6. Водитель доставил коробку с виноградом на автоматический участок отжима. Водитель вскрывает коробку и высыпает виноград в резервуар Умного пресса. Водитель указывает штрихкод упаковки, адрес пресса, создает транзакцию на передачу коробки, подписывает ее. Умный пресс с адресом 0x4fde31e09266423d5f1b8bf16dc8def085c197e5 взвешивают коробку. Автоматические весы создают и подписывают своим закрытым ключом транзакцию на изменение данных:

|id участка|Идентификатор упаковки|Количество|Сотрудник/Робот|
|----------|----------|----------|----------|
|spyfvqwnd|1E09266423d5f1B8b|0|0xf3101865bd9dbe720464e684247a13269cca70660xf|
|spyfvqwnd|1E09266423d5f1B8b|30|0x4fde31e09266423d5f1b8bf16dc8def085c197e5|

Фактически 30 кг винограда были переданы от Водителя Автоматическому прессу.

7. Из резервуара для взвешивания виноград попадает в резервуар для отжима с идентификатором 5f1b8bf16dc8de. Умный пресс создает и подписывает транзакцию и происходят следуюшие изменения.

|id участка|Идентификатор упаковки|Количество|Сотрудник/Робот|
|----------|----------|----------|----------|
|spyfvqwnd|1E09266423d5f1B8b|0|0x4fde31e09266423d5f1b8bf16dc8def085c197e5|
|spyfvqwnd|5f1b8bf16dc8de|30|0x4fde31e09266423d5f1b8bf16dc8def085c197e5|

Фактически 30 кг винограда из коробки были перемещены в резервуар для отжима.

8. При этом в резервуаре в итоге оказывается 100 кг винограда с трех участков и в блокчейне мы видим следующее:

|id участка|Идентификатор упаковки|Количество|Сотрудник/Робот|
|----------|----------|----------|----------|
|spyfvqwnd|5f1b8bf16dc8d|30|0x4fde31e09266423d5f1b8bf16dc8def085c197e5|
|spyfvqwn6|5f1b8bf16dc8d|30|0x4fde31e09266423d5f1b8bf16dc8def085c197e5|
|spyfvqwng|5f1b8bf16dc8d|40|0x4fde31e09266423d5f1b8bf16dc8def085c197e5|

9. Умный пресс произвел отжим и получил 100 литров виноградного сока. Умный пресс создает транзакцию на перемещение 100 литров сока и подписывает ее. По трубам сок попадает в цистерну для брожения. Цистерная имеет идентификатор 1f7b8bs1ddcld. Умный датчик объема жидкости с адресом 0x640bF693d3c06599300c1E2Be38c7F4AbCc597a1 подписывает транзакцию  и происходят следующие изменения:

|id участка|Идентификатор упаковки|Количество|Сотрудник/Робот|
|----------|----------|----------|----------|
|spyfvqwnd|5f1b8bf16dc8d|0|0x4fde31e09266423d5f1b8bf16dc8def085c197e5|
|spyfvqwn6|5f1b8bf16dc8d|0|0x4fde31e09266423d5f1b8bf16dc8def085c197e5|
|spyfvqwng|5f1b8bf16dc8d|0|0x4fde31e09266423d5f1b8bf16dc8def085c197e5|
|spyfvqwnd|1f7b8bs1ddcld|30|0x640bF693d3c06599300c1E2Be38c7F4AbCc597a1|
|spyfvqwn6|1f7b8bs1ddcld|30|0x640bF693d3c06599300c1E2Be38c7F4AbCc597a1|
|spyfvqwng|1f7b8bs1ddcld|40|0x640bF693d3c06599300c1E2Be38c7F4AbCc597a1|

10. В чане для брожения общий объем 684 литра. 

|id участка|Идентификатор упаковки|Количество|Сотрудник/Робот|
|----------|----------|----------|----------|
|spyfvqwnd|1f7b8bs1ddcld|30|0x640bF693d3c06599300c1E2Be38c7F4AbCc597a1|
|spyfvqwn6|1f7b8bs1ddcld|30|0x640bF693d3c06599300c1E2Be38c7F4AbCc597a1|
|spyfvqwng|1f7b8bs1ddcld|40|0x640bF693d3c06599300c1E2Be38c7F4AbCc597a1|
|все остальные id участков|1f7b8bs1ddcld|584|0x640bF693d3c06599300c1E2Be38c7F4AbCc597a1|

11. После брожения 684 литров вина разливается по 3 бочкам. Идентификаторы бочек 1f7b8bs1ddcln, 5f7b8hs1dscld, 2f7bfs1ddcld.

12. Розлив осуществляет рабочий вручную. Рабочий имеет адрес 0xb32242B1353638ffE3485ab523b5ed8C0522595B. Умный резервуар создает транзакцию на передачу 684 литров вина. Рабочий осуществляет розлив, создает и подписыват транзакцию на то, что он разлил вино в 3 бочки.

|id участка|Идентификатор упаковки|Количество|Сотрудник/Робот|
|----------|----------|----------|----------|
|spyfvqwnd|1f7b8bs1ddcld|0|0x640bF693d3c06599300c1E2Be38c7F4AbCc597a1|
|spyfvqwn6|1f7b8bs1ddcld|0|0x640bF693d3c06599300c1E2Be38c7F4AbCc597a1|
|spyfvqwng|1f7b8bs1ddcld|0|0x640bF693d3c06599300c1E2Be38c7F4AbCc597a1|
|все остальные id участков|1f7b8bs1ddcld|0|0x640bF693d3c06599300c1E2Be38c7F4AbCc597a1|
|spyfvqwnd|1f7b8bs1ddcln|10|0xb32242B1353638ffE3485ab523b5ed8C0522595B|
|spyfvqwn6|1f7b8bs1ddcln|10|0xb32242B1353638ffE3485ab523b5ed8C0522595B|
|spyfvqwng|1f7b8bs1ddcln|13.3|0xb32242B1353638ffE3485ab523b5ed8C0522595B|
|все остальные id участков|1f7b8bs1ddcln|194.7|0xb32242B1353638ffE3485ab523b5ed8C0522595B|
|spyfvqwnd|5f7b8hs1dscld|10|0xb32242B1353638ffE3485ab523b5ed8C0522595B|
|spyfvqwn6|5f7b8hs1dscld|10|0xb32242B1353638ffE3485ab523b5ed8C0522595B|
|spyfvqwng|5f7b8hs1dscld|13.3|0xb32242B1353638ffE3485ab523b5ed8C0522595B|
|все остальные id участков|5f7b8hs1dscld|194.7|0xb32242B1353638ffE3485ab523b5ed8C0522595B|
|spyfvqwnd|2f7bfs1ddcld|10|0xb32242B1353638ffE3485ab523b5ed8C0522595B|
|spyfvqwn6|2f7bfs1ddcld|10|0xb32242B1353638ffE3485ab523b5ed8C0522595B|
|spyfvqwng|2f7bfs1ddcld|13,3|0xb32242B1353638ffE3485ab523b5ed8C0522595B|
|все остальные id участков|2f7bfs1ddcld|194.7|0xb32242B1353638ffE3485ab523b5ed8C0522595B|

13. После выдержки вино из одной бочки автоматически разливается по бутылкам обьемом 0,75 л. Рабочий устанавливает бочку 1f7b8bs1ddcln в аппарат для розлива, создает и подписывает транзакцию на розлив вина. Автоматически аппарат с адресом 0x32Be343B94f860124dC4fEe278FDCBD38C102D88 разливает бочку по бытылкам, создает и подписывает транзакцию. Каждая бутылка имеет уникальный идентификатор. Происходят следующие изменения:

|id участка|Идентификатор упаковки|Количество|Сотрудник/Робот|
|----------|----------|----------|----------|
|spyfvqwnd|1f7b8bs1ddcln|0|0xb32242B1353638ffE3485ab523b5ed8C0522595B|
|spyfvqwn6|1f7b8bs1ddcln|0|0xb32242B1353638ffE3485ab523b5ed8C0522595B|
|spyfvqwng|1f7b8bs1ddcln|0|0xb32242B1353638ffE3485ab523b5ed8C0522595B|
|все остальные id участков|1f7b8bs1ddcln|0|0xb32242B1353638ffE3485ab523b5ed8C0522595B|
|spyfvqwnd|4f7bns1dlclr|0.03|0xb32242B1353638ffE3485ab523b5ed8C0522595B|
|spyfvqwn6|4f7bns1dlclr|0.03|0xb32242B1353638ffE3485ab523b5ed8C0522595B|
|spyfvqwng|4f7bns1dlclr|0.03|0xb32242B1353638ffE3485ab523b5ed8C0522595B|
|все остальные id участков|4f7bns1dlclr|0.64|0xb32242B1353638ffE3485ab523b5ed8C0522595B|
|все остальные id участков|все остальные бутылки|227.25|0xb32242B1353638ffE3485ab523b5ed8C0522595B|

14. На полке магазина любой пользователь может зайти в приложение. Указать номер бутылки 4f7bns1dlclr и получить информацию о том, что вино из этой бутылки сделано из винограда, который был выращен здесь:

|Бутылка|Участок|Количество|
|------|------|---------|
|1f7b8bs1ddcln|[spyfvqwnd](https://explorer.galtproject.io/map/#spyfvqwnd)|0.03|
|1f7b8bs1ddcln|[spyfvqwn6](https://explorer.galtproject.io/map/#spyfvqwn6)|0.03|
|1f7b8bs1ddcln|[spyfvqwng](https://explorer.galtproject.io/map/#spyfvqwng)|0.03|
|1f7b8bs1ddcln|другие участки|0.64|

Достоверность этих данных будет гарантирована криптографической защитой.







