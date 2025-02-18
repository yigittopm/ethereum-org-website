---
title: Развертывание собственного узла Ethereum
description: Общее введение в запуск собственного экземпляра клиента Ethereum.
lang: ru
sidebarDepth: 2
---

Запуск собственного узла дает вам различные преимущества, открывает новые возможности и помогает поддерживать экосистему. Эта страница поможет вам развернуть собственный узел и принять участие в проверке транзакций Ethereum.

## Прежде чем начать {#prerequisites}

Вы должны понимать, что такое узел Ethereum и почему вам может понадобиться запустить клиент. Это описано в статье [Узлы и клиенты](/developers/docs/nodes-and-clients/).

Если тема запуска собственного узла для вас новая или вы ищете менее «технический» способ, посмотрите наш более понятное для новичков [введение в запуск узлов Ethereum](/run-a-node).

## Выбор подхода {#choosing-approach}

Первый шаг в разворачивании вашего узла — выбор подхода. Вы должны выбрать клиент (программное обеспечение), среду и параметры, с которыми хотите начать. Просмотрите все доступные [клиенты основной сети](/developers/docs/nodes-and-clients/#advantages-of-different-implementations).

### Настройки клиента {#client-settings}

Реализации клиента включают различные режимы синхронизации и многие другие параметры. [Режимы синхронизации](/developers/docs/nodes-and-clients/#sync-modes) представляют собой различные методы загрузки и проверки данных блокчейна. Перед запуском узла следует решить, какую сеть и режим синхронизации использовать. Наиболее важно учитывать дисковое пространство и время синхронизации, которые потребуются клиенту.

Все функции и опции можно найти в документации клиента. Различные конфигурации клиента можно установить, запустив клиент с соответствующими флагами. В целях тестирования вы можете запустить клиент в одной из тестовых сетей. [Обзор поддерживаемых сетей](/developers/docs/nodes-and-clients/#execution-clients).

### Среда и оборудование {#environment-and-hardware}

#### Локально или в облаке {#local-vs-cloud}

Клиенты Ethereum могут работать на компьютерах потребительского класса и не требуют специального оборудования (например, в отличие от майнинга). Таким образом, в зависимости от ваших нужд вам доступны различные способы развертывания. Для упрощения давайте рассмотрим запуск узла как на локальной физической машине, так и на облачном сервере.

- Облако
  - Провайдеры предлагают большое время безотказной работы сервера и статические общедоступные IP-адреса
  - Получение выделенного или виртуального сервера может быть более удобным, чем создание собственного
  - Необходимость доверяться третьей стороне — поставщику серверов
  - Из-за большого размера хранилища для полного узла цена арендованного сервера может быть высока
- Собственное оборудование
  - Более независимый подход, требующий меньшего доверия посторонним
  - Однократное вложение
  - Возможность покупки преднастроенной машины
  - Необходимость подготовить и обслуживать оборудование, а также устранять возможные проблемы

Оба варианта имеют различные преимущества, описанные выше. Если вы ищете облачное решение, помимо многих традиционных поставщиков облачных вычислений есть сервисы, ориентированные на развертывание узлов. Например:

- [Узлы](https://www.quiknode.io/)
- [Blockdaemon](https://blockdaemon.com)
- [LunaNode](https://www.lunanode.com/)
- [Alchemy](https://www.alchemy.com/)

#### Аппаратное обеспечение {#hardware}

Однако устойчивая к цензуре децентрализованная сеть не должна полагаться на облачных провайдеров. Для экосистемы будет полезнее, если вы запустите свой узел на собственном оборудовании. Самыми простыми вариантами являются преднастроенные машины, такие как:

- [DappNode](https://dappnode.io/)
- [Avado](https://ava.do/)

Проверьте минимальные и рекомендуемые [требования к дисковому пространству для каждого клиента и режима синхронизации](/developers/docs/nodes-and-clients/#requirements). Обычно для этого достаточно довольно скромной вычислительной мощности. Проблема обычно заключается в скорости диска. Во время начальной синхронизации клиенты Ethereum выполняют множество операций чтения и записи. Поэтому настоятельно рекомендуется использовать SSD. Клиент может даже не иметь [возможности синхронизировать текущее состояние на HDD диске](https://github.com/ethereum/go-ethereum/issues/16796#issuecomment-391649278), застревая в нескольких блоках позади основной сети. Большинство клиентов можно запустить на [одноплатном компьютере с ARM](/developers/docs/nodes-and-clients/#ethereum-on-a-single-board-computer/). Вы также можете использовать операционную систему [Ethbian](https://ethbian.org/index.html) для Raspberry Pi 4. Это позволит вам [запустить клиент с SD-карты](/developers/tutorials/run-node-raspberry-pi/). В зависимости от выбранного вами программного и аппаратного обеспечения время первоначальной синхронизации и требования к объему хранилища могут различаться. Обязательно [проверьте время синхронизации и требования к хранилищу](/developers/docs/nodes-and-clients/#recommended-specifications). Также убедитесь, что у вашего интернет-соединения нет [ограничения пропускной способности](https://wikipedia.org/wiki/Data_cap). Рекомендуется использовать безлимитное соединение, так как первоначальная синхронизация и обмен данными с сетью могут превысить ваш лимит.

#### Операционная система {#operating-system}

Все клиенты поддерживают основные операционные системы — Linux, MacOS, Windows. Это означает, что вы можете запускать узлы на обычных настольных компьютерах или серверах с операционной системой (ОС), которая подходит вам лучше всего. Убедитесь, что ваша ОС обновлена, чтобы избежать потенциальных проблем и уязвимостей.

## Раскрутка узла {#spinning-up-node}

### Получение клиентского программного обеспечения {#getting-the-client}

Сначала скачайте [клиентское программное обеспечение](/developers/docs/nodes-and-clients/#execution-clients)

Вы можете просто скачать исполняемое приложение или установочный пакет, который подходит вашей операционной системе и архитектуре. Всегда проверяйте подписи и контрольные суммы скачанных пакетов. Некоторые клиенты также предлагают репозитории для упрощения установки и обновления. Если хотите, можете сами собрать из исходников. Все клиенты имеют открытый исходный код, поэтому вы можете собрать их из исходного кода с помощью соответствующего компилятора.

Исполняемые файлы для стабильных реализаций клиентов основной сети можно загрузить со страниц их выпусков:

- [Geth](https://geth.ethereum.org/downloads/)
- [OpenEthereum](https://github.com/openethereum/openethereum/releases)
- [Nethermind](https://downloads.nethermind.io/)
- [Besu](https://besu.hyperledger.org/en/stable/)
- [Erigon](https://github.com/ledgerwatch/erigon)

**Обратите внимение, что OpenEthereum [устарел](https://medium.com/openethereum/gnosis-joins-erigon-formerly-turbo-geth-to-release-next-gen-ethereum-client-c6708dd06dd) и больше не поддерживается.** Используйте его с осторожностью и по возможности перейдите на другую реализацию клиента.

### Запуск клиента {#starting-the-client}

Перед запуском клиентского программного обеспечения Ethereum убедитесь что ваша среда готова. Например, убедитесь в следующем:

- На диске достаточно места с учетом выбранной сети и режима синхронизации.
- Память и ЦП не нагружаются другими программами.
- Операционная система обновлена до последней версии.
- В системе установлены правильное время и дата.
- Ваш маршрутизатор и брандмауэр принимают подключения к прослушиваемым портам. По умолчанию клиенты Ethereum используют порт слушателя (TCP) и порт обнаружения (UDP), оба по умолчанию 30303.

Сначала запустите свой клиент в тестовой сети, чтобы убедиться, что все работает правильно. [Инструкции по запуску легкого узла Geth](/developers/tutorials/run-light-node-geth/) должны помочь. Необходимо указать все настройки клиента, которые не установлены по умолчанию. Вы можете использовать конфигурационный файл, чтобы определить свой набор настроек. Конкретные настройки можно найти в документации вашего клиента Исполнение клиента запустит его базовые функции и выбранные конечные точки, а затем начнется поиск узлов одноранговой сети. Когда узел найдет одноранговые соединения, клиент начнет синхронизацию. Актуальные данные блокчейна будут доступны, как только клиент закончит синхронизацию до текущего состояния.

### Использование клиента {#using-the-client}

Клиенты предоставляют конечные точки RPC API, которые можно использовать для управления клиентом и взаимодействием с сетью Ethereum различными способами:

- Вызывать API вручную через наиболее подходящий протокол (например, через `curl`)
- Подсоединять предоставленную консоль (например, `geth attach`)
- Использовать в приложении

У разных клиентов различаются реализации конечных точек RPC. Но существует стандарт JSON-RPC, которые можно использовать с любым клиентом. Обзор приведен в [документации JSON-RPC](https://eth.wiki/json-rpc/API). Приложения, которым требуется информация из сети Ethereum, могут использовать этот RPC. Например, популярный кошелек MetaMask позволяет вам [запустить локальный узел и присоединиться к нему](https://metamask.zendesk.com/hc/en-us/articles/360015290012-Using-a-Local-Node).

#### Доступ к RPC {#reaching-rpc}

Порт JSON-RPC по умолчанию — `8545`, но порты локальных конечных точек можно изменять в конфигурационном файле. По умолчанию интерфейс RPC доступен только с локального хоста компьютера. Чтобы сделать его доступным удаленно, можно сделать его открытым, сменив адрес на `0.0.0.0`. Это сделает ваш узел доступным для локальных и публичных IP-адресов. В большинстве случаев вам также нужно настроить переадресацию портов на маршрутизаторе.

Совершать подобные манипуляции нужно с осторожностью, так как это позволит любому в Интернете управлять вашим узлом. Злонамеренные пользователи, имея доступ к вашему узлу, могут навредить системе или украсть ваши активы, если вы используете свой клиент как кошелек.

Эту проблему можно решить, предотвратив изменение потенциально опасных методов RPC. Например, в `geth` можно задать методы, которые можно будет использовать для модификации, через опцию командной строки: `--http.api web3,eth,txpool`.

Вы также можете размещать доступ к RPC интерфейсу, указывая службу веб-сервера, например Nginx, на локальный адрес и порт вашего клиента.

Наиболее конфиденциальный и одновременно простой способ настроить публично доступную конечную точку — развернуть ее как сервис onion [Tor](https://www.torproject.org/). Это позволит вам получать доступ к RPC за пределами вашей локальной сети без статического публичного IP-адреса или открытых портов. Для этого:

- Установите `tor`
- Отредактируйте конфигурационный файл `torrc`, чтобы настроить скрытую службу с адресом и портом вашего RPC клиента
- Перезапустите службу `tor`

После перезапуска Tor вы получите имя хоста и ключи скрытой службы в желаемой директории. С этого момента ваш RPC будет доступен в сети Tor по своему имени хоста `.onion`.

### Управлением узлом {#operating-the-node}

Вы должны регулярно проверять свой узел, чтобы убедиться, что он работает правильно. Время от времени может быть необходимо проводить техническое обслуживание.

#### Поддержание работы узла в сети {#keeping-node-online}

Ваш узел необязательно должен быть постоянно подключен к сети, но желательно держать его в сети как можно дольше, чтобы поддерживать его синхронизацию с сетью. Вы можете отключить его для перезапуска, но имейте в виду:

- Завершение работы может занять несколько минут, если последнее состояние все еще записывается на диск.
- Принудительное отключение может повредить базу данных.
- Ваш клиент не будет синхронизироваться с сетью, и при перезапуске потребуется повторная синхронизация.

_Это не относится к узлам-валидаторам слоя консенсуса._ Выключение вашего узла повлияет на все службы, которые от него зависят. Если вы запускаете узел для _стейкинга_, вы должны минимизировать время простоя, насколько это возможно.

#### Создание клиентской службы {#creating-client-service}

Рассмотрим возможность создания службы для автоматической активации клиента при запуске. Например, на серверах Linux хорошим решением будет создание службы, которая выполняет клиент с определенной конфигурацией от имени пользователя с ограниченными правами и перезапускается автоматически.

#### Обновление клиента {#updating-client}

Вам необходимо постоянно обновлять клиентское программное обеспечение последними исправлениями безопасности, функциями и [EIP](/eips/). Перед [хард-форками](/history/) обязательно нужно убедиться, что вы используете правильную версию клиента.

Каждая реализация клиента имеет человекочитаемую строку версии, используемой в протоколе одноранговой связи, но она также доступна из командной строки. Эта строка версии позволяет пользователям убедиться, что они используют правильную версию, и использовать обозреватели блоков и другие аналитические инструменты, задействованные в количественной оценке распространения определенных клиентов в сети. Более подробную информацию о строках версии можно получить в документации к конкретному клиенту.

#### Запуск дополнительных служб {#running-additional-services}

Запуск собственного узла дает возможность вашим службам использовать прямой доступ к клиентскому RPC сети Ethereum. Такие службы построены поверх Ethereum, примером чего могут быть [решения слоя 2](/developers/docs/scaling/#layer-2-scaling), [консенсус-клиенты](/developers/docs/nodes-and-clients/#consensus-clients) и другие части инфраструктуры Ethereum.

#### Наблюдение за узлом {#monitoring-the-node}

«Чтобы правильно организовать наблюдение за узлом, представьте сбор метрик. Клиенты предоставляют конечные точки с метриками, и вы можете получить сравнительные данные о вашем узле. Используйте инструменты, подобные [InfluxDB](https://www.influxdata.com/get-influxdb/) или [Prometheus](https://prometheus.io/), для создания баз данных, которые вы можете превратить в визуализации и графики через такие инструменты, как [Grafana](https://grafana.com/). Вы можете использовать это программное обеспечение и другие панели Graphana в различных конфигурациях, чтобы визуализировать свой узел и всю сеть в целом. При отслеживании всегда обращайте внимание на производительность вашей системы. Во время первоначальной синхронизации узла клиентская программа может оказывать очень большую нагрузку на процессор и оперативную память. В дополнение к Graphana вы можете использовать инструменты, которая предлагает ваша операционная система, подобные `htop` или `uptime`.

## Дополнительные ресурсы {#further-reading}

- [Анализ требований к оборудованию, чтобы стать полностью проверенным узлом Ethereum](https://medium.com/coinmonks/analyzing-the-hardware-requirements-to-be-an-ethereum-full-validated-node-dc064f167902) — _Альберт Палау, 24 сентября 2018 г._
- [Запуск полных узлов Ethereum: руководство для сомневающихся](https://medium.com/@JustinMLeroux/running-ethereum-full-nodes-a-guide-for-the-barely-motivated-a8a13e7a0d31) — _Джастин Леру, 7 ноября 2019 г._
- [Запуск узла Hyperledger Besu в основной сети Ethereum: преимущества, требования и настройка](https://pegasys.tech/running-a-hyperledger-besu-node-on-the-ethereum-mainnet-benefits-requirements-and-setup/) — _Фелипе Фараджи, 7 мая 2020 г._
- [Развертывание клиента Nethermind Ethereum со стеком мониторинга](https://medium.com/nethermind-eth/deploying-nethermind-ethereum-client-with-monitoring-stack-55ce1622edbd) _— Nethermind.eth, 8 июля 2020 г._

## Похожие темы {#related-topics}

- [Узлы и клиенты](/developers/docs/nodes-and-clients/)
- [Блоки](/developers/docs/blocks/)
- [Сети](/developers/docs/networks/)
