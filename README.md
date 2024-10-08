Привет, друзья. Сегодня я практически в лайв режиме расскажу как безболезненно настроить и подключить себе ВПН. На всякий случай рекомендую самостоятельно провести исследование темы, потому что я не специалист в этой области, а то, как вы заигрываете с лучшим другом пока месите жуков в Helldivers уже та информация, которую вы хотите сохранить. Данный метод прост, но аудит безопасности системы я не проводил

Топики этой пасты такие: 
1. Вводная
2. Как купить крипту для оплаты сервера (для самых маленьких)
2. Аренда VPS и его оплата
3. Разворачивание ВПНа и настройка клиента

# ВВЕДЕНИЕ

С VPN в России в нынешнее время есть нюансы. Самый важный из них - блокируют не сервисы, которые вам предоставляют услуги, а протоколы. Это значит, что даже если вы нашли хороший OpenVPN сервис, который смог модифицировать протокол - уже совсем скоро он отвалится так же как и остальные

В таких условиях мы хотим не только подключиться, а замаскировать своё подключение и сам протокол под вид обычной деятельности в интернете и таких методов существует, например Cloack который позволяет замаскировать ваше OpenVPN или Shadowsocks подключение, но настройки такого подключения на клиенте сложнее

Я же выбрал Xray Reality, разработка братушек китайцев, которые очень любят обходить Великий Китайский Файерволл из-за актуальности, опенсорсности и простоты подключения. О нём и пойдет речь
Репо, можете отдать своему другу кодеру на изучение:
https://github.com/XTLS/Xray-core 

Получилось обойтись десятком комманд в терминале и одной копипастой конфига, так что сложно не будет.

Важно – если не хотите морочиться с криптой, переходите сразу к пункту 3, но ваш выбор будет несколько ограничен

# ВЫБОР VPS СЕРВЕРА

Для начала нам нужно заиметь себе **VPS** - Virtual Private Server. Методов поиска таковых много, главные рекомендации такие:
1. Находится в нужной нам стране
2. Принимает оплату в крипте. Есть те,  кто принимает российские карты, но безопасность и надежность такого решения остается за вами, любой провайдер может в любой момент отказать вам в оплате
3. Не говно - всё просто и одновременно сложно. Смотрим отзывы и ищем честные

Для тестов сегодня я остановился на Monovm, они принимают оплату в удобном формате и предоставляют разумные цены

Ищем где мы можем подключить себе VPS. В моём случае он самый простой и дешевый с локацией в Амстердаме, выбираем образ AlmaLinux/Ubuntu/Debian/CentOS. Конечный выбор не принципиален, главное линукс
В моём случае это Alma с дефолтными настройками

![image](https://github.com/user-attachments/assets/2f21536b-4f58-4123-bd82-c46b086df557)

В данный момент оплатить мы его не можем, но уже знаем, сколько он будет стоить. Сейчас нам нужно немного опередить события и пройти до этапа оплаты, не оплачивая сервер, чтобы узнать какой именно криптой мы можем воспользоваться

![image](https://github.com/user-attachments/assets/78537427-044d-47a5-8baf-99932a70dab0)

В моём случае вариантов много, но самым лучшим из них будет **USDT** **TRC20**, он же **Tron**

![image](https://github.com/user-attachments/assets/561f24f0-70d7-413d-a133-f80867a3f960)

Краткий ликбез
Разные криптовалюты можно проводить через разные сети и комиссии там так же отличаются. Самый простой и удобный способ именно USDT в сети TRC20, потому что комса там минимальна, а покупать мы и так будем USDT.
Если такого варианта нет, перейдите к процессу создания аккаунта на бирже и я скажу когда мы сюда вернемся

# КРИПТА ДЛЯ ОПЛАТЫ

Механика здесь проста: У вас есть карта банка, у кого-то есть нужные нам монетки, будем обмениваться. Для этого нужно выбрать биржу и использовать **P2P** (peer to peer) торговлю.
Я уже давно пользуюсь Bitget, вы же можете уже знать другие биржи и пользоваться ими, но есть пара нюансов

1. Не рекомендую ByBit, знаю нескольких людей с заблокированными без причин аккаунтами
2. Binance не работает с россиянами
3. Не выбирайте нонеймов

Процесс регистрации на бирже простой, но включает в себя Know Your Customer - от вас попросят фотку паспорта и лица. Это нормальная практика, если вас смущает, то оплата криптой будет сложнее, придется разбираться самому, можно попробовать через telegram wallet

Зарегались и дождались аппрува - идем покупать. Процесс не без нюансов, так как мы работаем с людьми и хотим избежать скама. Лично я не знаю людей, которым блокировали карты за бытовое использование P2P и сам ежемесячно так отправляю деньги в  РФ, но имейте в виду, что это не мы работаем с людьми, которые могут отмывать бабки.

## Если на прошлом этапе вы не смогли найти USDT через TRC20

- Найдите в шапке сайта свой кошелёк (Это может быть пункт assets или просто иконка кошелька), наведите на него и выберите Widthraw
- В пункте Select a coin выберите одну из монет представленных на сайте оплаты, например Bitcoin
- В пункте Select network ищите сеть, в которой сервис просит оплату. Если она есть, всё отлично. Если нет, можете погуглить название сети, чтобы узнать альтернативные названия. Так, TRC20 может быть Tron или TRX. Обратите внимание на комиссию,если она вас не устраивает, попробуйте любую другую монету

![image](https://github.com/user-attachments/assets/4b879418-c486-4bff-9a78-3be836a042e2)

- В шапке сайта найдите Trade -> Convert. В меню выберите конвертацию из USDT в нужную вам монету и оцените комиссию. Она может быть и нулевая

![image](https://github.com/user-attachments/assets/844815f2-21e5-4f75-a4a8-ff811e4cb972)
![image](https://github.com/user-attachments/assets/3c75ab1e-c4c7-4ea4-b3bc-7a161685d275)

Те две комиссии, которые мы узнали, нужно будет учитывать при покупке крипты.

## Идём дальше

Сейчас лучший момент, чтобы не проводить реальную операцию, а просто прочитать эту часть гайда и потыкать интерфейс, не доводя до создания ордера. Если вам что-то будет непонятно - просто загуглите "Как купить крипту P2P на *название биржы*". Помимо бирж, которые предоставляют пошаговые инструкции,  есть пользователи, которые так же пишут туториалы.

Нужно помнить что при переводе денег в крипте взимается комиссия. В моём случае сервер стоил 13 баксов в месяц. Сумма в USDT будет почти такая же, но с некоторым плаванием в долях центов. Тем не менее оплатить нужно именно столько, сколько сказано. При расчёте того, сколько денег вам нужно перевести всегда учитывайте комиссии. В случае с USDT через TRC20 это где то 1-1.5 бакса, в иных случаях мы уже всё просчитали. Лучше переплатить 50-100 рублей, чем потом не иметь возможность докинуть их, потому что никто не работает с копеечными суммами

- Заходим на сайт и ищем раздел Buy Crypto -> P2P trading
- Валюту выбираем RUB, битгет в таком случае переносит нас на поддомен
- Выбираем Buy, вводим нужный нам Sell Amount в рублях, ставим show merchant ads (если есть, это означает что отображаться будут только верифицированные менялы) и выбираем Payment method. В случае опять же битгета, local card yellow это тиньк, а green -сбер.

![image](https://github.com/user-attachments/assets/9170f96b-e8b0-4b16-b8f8-e4f52b872445)

-  Выбираем мерчанта по цене и совершенным сделкам и жмаем Buy.

![image](https://github.com/user-attachments/assets/e1790c00-dd13-49c8-ba65-495b9d184966)


В появившемся окне вводим сумму **В USDT** которую планируем получить. С учётом комиссии за перевод и конвертацию (если она нужна). Опять же, лучше перебздеть чем недобздеть, тем более, если вы планируете и далее оплачивать этот сервис таким методом.
*Внимательно* читаем что человек написал в комментарии, возможно вы не сможете перевести ему деньги, потому что он забыл убрать ваш метод оплаты и уже не принимает его. Если не написано ничего - после открытия ордера посмотрите, не напишет ли он что-либо в чат

На этом моменте биржа может запросить от вас сгенерировать дополнительный пароль для таких операций или провести ещё какие то действия. Пароли не забываем записать, они нам пригодятся.

Когда откроется сделка, вам будет сказано куда платить. Если что-то непонятно, спросите у продавца, ему ваши деньги нужны, чаще всего нужно просто скинуть на карту дропа указанную вами же сумму, подтвердить оплату и скинуть челу чек. Можно не особо переживать насчёт кидалова - во первых мы выбрали верифицированного мерчанта, во вторых всегда можно обратиться в поддержку с пруфами. На личном опыте - всегда всё было отлично, кроме одного раза, когда чел не мог подтвердить транзакцию в течение нескольких часов, чаще всего это дело 10-ти минут.

Как только вы отправили деньги, скачали чек и скинули его в чат, смело жмите подтвердить и ждите, когда продавец отпустит вам крипту. Иногда требуется ввести дополнительный пароль от кошелька, иногда просто код с почты или google authentificator, вариации разные, но это всё просто для того, чтобы и вы и продавец были чуть более уверенны в обоюдной честности.

Как только меняла подтвердил операцию, поздравляю, **самое сложное позади**

Идём в assets и ищем куда же нам пришли деньги. Чащё всего это **спотовый (spot)** кошёлек, он нам и нужен. Если их там нет, поищите по разделам и совершите transfer из того раздела, где вы обнаружили свои деньги в spot. Эта операция моментальна и бесплатна. В зависимости от настроек деньги можно обнаружить в Funding или Trading разделе.

Если вы купили USDT, а оплата нужна в чём то другом, по старинке идём в Convert и просто конвертируем одно в другое. Так же смотрите, какой кошелёк выбираете при конвертации, на Funding или Trading у нас теперь 0, всё на спотовом

![image](https://github.com/user-attachments/assets/59536663-0190-4a8b-b988-9400186541df)


## Оплачиваем сервер

На сайте сервера выбираем ту сеть и монету, через которую мы решили платить

![image](https://github.com/user-attachments/assets/1781e1c9-c811-4d4d-97de-93f91d47f87d)

Переходим к оплате. Лично я для гайда отрыл копейки с другой биржи, но подход везде одинаков. После нажания оплаты на сайте сервиса нам должны были показать детали, например так

![image](https://github.com/user-attachments/assets/9719df7f-5cc2-46a8-a847-469ded9e3689)

Нам нужно скопировать Address и перейти на нашей бирже в раздел widtraw -> crypto
Выбираем on-chain перевод, нужную нам монету и сеть. И **ВНИМАТЕЛЬНО** вставляем скопированный адрес. Проверьте его дважды глазами 

![image](https://github.com/user-attachments/assets/2dfaf6df-240a-4568-9c7b-a78feb838106)

Так же **ВАЖНО**. Введите сумму перевода и узнайте, сколько денег получится в итоге. На скрине я пользовался биржей OKX, которая по дефолту воспринимает введенную вами сумму как ту, которую вы хотите потратить, а не ту, которая будет в итоге. Нажав кнопку revert amount можно выбрать, что будет отображаться - сколько придёт или сколько потратите. Будьте уверены что в итоге вы переведете ровно столько сколько надо

Когда всё проверили - жмите перевод. Скорее всего потребуется подтверждение

![image](https://github.com/user-attachments/assets/85b9d735-290f-4bc5-9d14-eb5ae7e1b415)

На сайте оплаты придется просто подождать. Чаще всего можно поискать на предмет кнопки check transfer и залипать в страницу. Переводы в крипте требуют некоторого времени, в TRC20 это обычно всего пара минут
Когда оплата дойдёт, страница автоматически отобразит это и вы сможете вернуться обратно к сервису. Поздравляю, осталось немного

Скорее всего вам на почту пришло письмо от сервиса, в котором есть все нужные нам данные. Если нет - поищите на сайте. Что нам нужно

- ip address
- ssh port (если не нашли, можем попробовать и без него)
- root password (иногда под вас могли создать не root пользователя, в таком случае будет user и password)

Всё это мы себе сохраняем

# Настройка VPN

Если вы используете Windows - вам нужен WSL, имхо самый простой метод. Чаще всего достаточно просто открыть PowerShell от имени администратора и ввести
`wsl --install`

И на вашей винде будет мини линукс. Для 10 и 11 работает хорошо, но вот на всякий случай гайд с сайта мелкомягких
https://learn.microsoft.com/en-us/windows/wsl/install
Так же можно установить Putty, это сторонняя альтернатива, которая позволит нам подключиться к серверу, там все в виде кнопок и полей, разобраться будет просто

**Что нужно знать для работы с терминалом:**
- Чтобы скопировать – выделяем мышкой и делаем CTRL+SHIFT+C
- Чтобы вставить – делаем CTRL+SHIFT+V

Открываем wsl и пишем

`ssh -p ПОРТ root@АЙПИ`
Здесь нам очевидно нужно заменить АЙПИ на тот айпишник, который мы получили в письме или нашли на сайте, а ПОРТ - на порт

Если не нашли порт - уберем его и попробуем так
`ssh root@АЙПИ`

Так же, если нам выдали не root пользователя - замените root на юзернейм.

При подключении, скорее всего запросит подтверждение, просто пишем yes и вводим пароль для пользователя. Когда будете вводить – не удивляйтесь, что ничего не появляется, так и задумано, просто введите и тыкните enter

![image](https://github.com/user-attachments/assets/3c115d54-d203-45c0-8171-ba9e3d18d6ba)


## Потратим немного времени на базовую подготовку:

Поменяем пароль нашего пользователя (если не root, то наш юзернейм):
`passwd root`
После чего система попросит вас дважды ввести новый пароль

Вспоминаем, какой линукс мы выбрали. Если это был Debian/Unubtu сделаем так:
`sudo apt update -y`
`sudo apt install nano -y`

Если это был AlmaLinux
`sudo dnf update -y`
`sudo dnf install nano -y`

Если CentOS:
`sudo yum update -y`
`sudo yum install nano -y`

Этими строками мы: обновили пакеты нашей системы и установили (или увидели что он уже установлен) редактор nano. Можно пользоваться и vim, но нано ощутимо более дружелюбный для новичков

## Устанавливаем VPN

Установим XRay с Reality скриптом от разработчиков:
`bash -c "$(curl -L https://github.com/XTLS/Xray-install/raw/main/install-release.sh)" @ install`

Генерируем UID и ключи, они понадобятся для подключения

`/usr/local/bin/xray uuid`
Сохраняем айди

![image](https://github.com/user-attachments/assets/edce8a07-8801-4173-86b7-039243fdc76e)


`/usr/local/bin/xray x25519`
Сохраняем ключи. Первый – **приватный**, второй - **публичный**

![image](https://github.com/user-attachments/assets/c4f7a84d-ab03-4fcc-9506-af3e1b3d7a28)


Так же придумаем и куда нибудь запишем любой набор 8-и латинских букв. Я буду использовать `aabbccdd` потому что так сделано в гайде с которым я сверялся

Выбираем сайт, под который мы хотим замаскировать своё подключение. Прикол тут в том, что мы хотим не только иметь доступ к заблокированным ресурсам, но и **не палиться**, что мы используем впн. Можно выбрать любой сайт любой незаблокированной компании. Я выбрал

`www.microsoft.com`

Как варианты:
_www.samsung.com_
_www.asus.com_
_www.nvidia.com_
_www.google.com_

Хоть порнхаб

## Настраиваем VPN

Редактируем конфиг

`nano /usr/local/etc/xray/config.json`

Берем вот эту пасту и копируем ее в конфиг. Для вставки в nano используйте CTRL+SHIFT+V

```
{
  "log": {
    "loglevel": "info"
  },
  "routing": {
    "rules": [],
    "domainStrategy": "AsIs"
  },
  "inbounds": [
    {
      "port": 23,
      "tag": "ss",
      "protocol": "shadowsocks",
      "settings": {
        "method": "2022-blake3-aes-128-gcm",
        "password": "aaaaaaaaaaaaaaaabbbbbbbbbbbbbbbb",
        "network": "tcp,udp"
      }
    },
    {
      "port": 443,
      "protocol": "vless",
      "tag": "vless_tls",
      "settings": {
        "clients": [
          {
            "id": "GENERATED ID",
            "email": "user1@myserver",
            "flow": "xtls-rprx-vision"
          }
        ],
        "decryption": "none"
      },
      "streamSettings": {
        "network": "tcp",
        "security": "reality",
                "realitySettings": {
                        "show": false,
                        "dest": "CHOSEN WEBSITE:443",
                        "xver": 0,
                        "serverNames": [
                                "CHOSEN WEBSITE"
                        ],
                        "privateKey": "PRIVATE KEY",
                        "minClientVer": "",
                        "maxClientVer": "",
                        "maxTimeDiff": 0,
                        "shortIds": [
                                "SHORT ID"
                        ]
                }
      },
      "sniffing": {
        "enabled": true,
        "destOverride": [
          "http",
          "tls"
        ]
      }
    }
  ],
  "outbounds": [
    {
      "protocol": "freedom",
      "tag": "direct"
    },
    {
      "protocol": "blackhole",
      "tag": "block"
    }
  ]
}
```

Что здесь нужно изменить
GENERATED ID - меняем на ID который мы сгенерировали выше и сохранили себе
CHOSEN WEBSITE -меняем на сайт – маскировку, в моем случае это www.microsoft.com, их два
PRIVATE KEY – меняем на сгенерированый приватный ключ, он был первым из пары
SHORT ID – меняем на те 8 символов, которые вы придумали

Не нужно добавлять и удалять пробелы/новые строки

После чего жмаем CTRL+X и Enter – сохраним файл

Рестартуем службу впн 
`systemctl restart xray`

Если не пишет никакой ERROR значит всё отлично

## Добавление дополнительных пользователей

Если нужно дать отдельный доступ кому-то ещё, порядок действий прост

Снова генерируем uid и сохраняем себе
`/usr/local/bin/xray uuid`

Меняем конфигурационный файл

`nano /usr/local/etc/xray/config.json`

В раздел settings -> clients добавляем нового пользователя с соответствующим ему uid

```
{
  "id": "НОВЫЙ АЙДИ",
  "email": "user1@myserver",
  "flow": "xtls-rprx-vision"
}
```
**Важно** - при добавлении нового пользователя поставьте запятую после закрывающей фигурной скобки предыдущего, вот так
```
{
  "id": "GENERATED ID",
  "email": "user1@myserver",
  "flow": "xtls-rprx-vision"
},
{
  Новый юзер
}
```
Но в самом конце запятую уже не ставьте

**Для нового пользователя при настройке клиентского приложения UUID aka GENERATED ID будет уже вот этим, новым**


## Скачиваем и настраиваем клиент

Теперь нужно скачать клиент для подключения. Я выбрал Nekoray (он есть для винды и линукса) и v2rayNG для андроида, альтернативы есть вот здесь в разделе Клиенты для XRay Reality, так же можно и просто загуглить
https://docs.amnezia.org/ru/documentation/alternative-clients/
Примеры будут на основе Nekoray, скрины в v2rayNG так же приложу. Если где то затык - можно погуглить Setup VLESS VPN *название программы*

Порядок настройки клиента единообразен. Скачиваем нужную нам программу. Если это Nekoray - при открытии он спросит какой мы хотим движок, выбираем sing-box.
Открываем и создаем новый профиль. Где то это плюсик, где то пкм -> create new profile

Нам нужно подключение типа **VLESS** и вот такого формата настройки

![image](https://github.com/user-attachments/assets/272f40cc-77ef-4f2c-842b-41f7d9ec32ab)

Address: адрес нашего сервера
Port: 443

VLESS:
UUID: айди пользователя, который мы сгенерировали и вставляли как GENERATED ID
Flow: xtls-rprx-vision

Settings как на скрине
Обязательно настраиваем TLS и выбираем его как security. Это нам нужно для подмены при подключении, мы всё ещё хотим делать вид что сидим на порнхабе, а не подключаемся непонятно куда непонятно для чего
SNI - сайт, под который маскируем подключение
ALPN - h2

TLS Camouflage
Fingerprint - выберите хром или что по душе, я поставил firefox потому что им пользуюсь. Так мы будем подменять мета информацию о подключении
Reality Pbk - наш публичный ключ, мы его генерировали вместе с приватным
Reality Sid - всё те же 8 символов, которые мы придумали, у меня это aabbccdd

**Сам впн готов, можно подключаться и тестить, но лучше:**

Настроим маршрутизацию. Нам не нужно подключение, если мы используем отечественный сервис, так что создадим правила. Заходим в preferences -> routing settings
Во вкладке common делаем как на скриншоте

![image](https://github.com/user-attachments/assets/4abcd17d-55fe-4372-ae64-ffa039ffc582)

Во вкладке Simple route добавим опцию прямого подключения к серверам, которые geoip (он умеет распознавать ru) сочтёт российскими
Не тестил, но полагаю, что так же можно сделать и с **ua** и **by**

![image](https://github.com/user-attachments/assets/7df59e22-1f42-47a1-a9a6-08fa4d6f5a35)

Можно так же поиграться и попробовать в блок перечения Proxy и domains написать конкретные домены, к которым вы хотите стучаться под впн, например discord.com или instagram.com
Для более точной настройки можно погуглить домены интересующих вас сервисов, вдруг вам VPN нужен только для конкретного сервиса, а в остальном вы хотите выглядеть примерным гражданином


Так же кликнем Custom Route и добавим туда такое правило
```
{
    "rules": [
        {
            "domain_suffix": [
                ".ru"
            ],
            "outbound": "direct"
        }
    ]
}

```

![image](https://github.com/user-attachments/assets/a17406ef-a087-49a4-8b50-38f59c97789c)

Здесь мы делаем так: указываем сайты с доменом `.ru` как те, к которым нужно подключаться без vpn (onbound: direct)

Сохраняем, выходим, тестим
Для Яндекса и 2ip.ru мы в Тбилиси

![image](https://github.com/user-attachments/assets/126b56cf-8489-4f58-a4fb-9bc2b4c456ea)

![image](https://github.com/user-attachments/assets/0e3aa5a3-3a68-435d-a3a6-9aff3c6711aa)

А вот myip.com знает, что нет

![image](https://github.com/user-attachments/assets/b739e7d7-8b1c-4866-a19c-89fa85b42790)

Для расшаривания подключения можно кликнуть ПКМ -> share. В Nekoray есть возможность генерировать qr, копировать конфиг или ссылку на поключение. Их же можно просто импортнуть на мобилу нажав плюсик и выбрав или Scan QR или Paste from clipboard 
Скрины для android, если всё делаем руками:

![image](https://github.com/user-attachments/assets/62dc1032-ad49-4973-a6f2-c263d5eba5ee)

![image](https://github.com/user-attachments/assets/060b6f5a-d89b-4182-b0f4-a3d43e75b397)

![image](https://github.com/user-attachments/assets/52e79fd4-df1a-45fc-8c3c-f62146e85f32)

Настройки все те же
Для настройки прямого подключения к российским ip:

![image](https://github.com/user-attachments/assets/893b1550-7c9b-49e5-8608-fd6a504b9714)

![image](https://github.com/user-attachments/assets/c3726ee8-c6f3-414d-b239-9e0b3dcde246)

![image](https://github.com/user-attachments/assets/4004bae1-292f-4525-b0cf-c470213cb7b0)

(Я выбрал Locked опцию просто так, можно и руками включать)

![image](https://github.com/user-attachments/assets/35150fb9-88d7-4b0d-9331-ea34e6441557)

Радуемся, с телефона мы тоже не в Амстердаме по мнению яндекса

![image](https://github.com/user-attachments/assets/4c6a666d-8e91-4f21-8db6-d34e2c224250)

Но myip.com снова знает о нас чуть больше
