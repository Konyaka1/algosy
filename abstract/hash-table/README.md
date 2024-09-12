## Хэш функция
Задача: отобразить _множетсво_ последовательности байт **любой длины** в _множество_ байт **фиксированный длины**.
### Виды
1) Криптографические. Устойчивы к коллизиям и к восстановлению данных из хэша.
2) Некриптографияесие. Общее назначение, высокая скорость и устойчивость к коллизиям. Нет необходимости к защите данных от восстановления по хэшу
3) Контрольные суммы. Простые функции проверяющие случайные ошибки при передаче данных. нет устойчивости к коллизиям и восстановлению/подмены данных
4) Перфектные хеш-функции. Функции на известном наборе входных значений. 100% Отсутсвие коллизий.


## JWT vs MD5
MD5 **одностороння** хэш функция, то есть невозможно восстановить данные из хэша

JWT двустороння функция, возможно восстановить данные имея необходимый ключ. Ключ не доступен публично, хранится на сервере выдавшем JWT.

JWT токен это строка, состаящая из `header.payload.signature`
- header -> хранит информацию о типе токена и алгоритме подписи
- payload -> закадированный json с инфрмацией (claims) о пользователе: айди, роли и тд.
- signature -> цифровая подпись. Используется для верификации подлинности токена на сервере


## Consistent hashing
Каждый бакет в таблице отвечает за отрезок хэшей. например от 5 до 17. Все ключи имеющие хэш от 5 до 17 попадут в этот бакет.

При решардинге это позволяет экономить ресурсы на перемещение данных из бакета в бакет.

#### Пример с добавлением бакета
- Бакет_1 хранит [0, 10]
- Бакет_2 хранит [11, 30]
- Бакет_3 хранит [31, 40]
- Бакет_4 хранит [41, 50]

Мы хотим добавить Бакет_5, который хранит [21, 30]. 
Для этого нам надо взять все данные из бакета2, у которых хэш от 21 до 30 и поместить в новый бакет.

#### Пример с удалением бакета
- Бакет_1 хранит [0, 10]
- Бакет_2 хранит [11, 20]
- Бакет_3 хранит [21, 30]
- Бакет_4 хранит [31, 40]
- Бакет_5 хранит [41, 50]

Мы хотим добавить Бакет_4, который хранит [31, 40]. 
Для этого нам надо решить какой бакет будет иметь больший диапазон.
Выбираем 3. Теперь третий бакет хранит [21, 40]. И мы закидываем все данные из бакет4 в бакет3.

Получается, что из всей системы перемещается только часть данных.
