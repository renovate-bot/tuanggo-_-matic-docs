---
id: what-is-polygon
title: Что такое Polygon?
description: Узнайте о решении масштабирования Polygon
keywords:
  - docs
  - matic
  - polygon
  - blockchain
  - ethereum scaling
image: https://wiki.polygon.technology/img/polygon-wiki.png
---

[Polygon](https://polygon.technology/) — это решение для масштабирования уровня 2, которое обеспечивает масштабирование за счет использования сайдчейнов для вычислений вне цепочки и децентрализованной сети валидаторов Proof-of-Stake (PoS).

Polygon стремится решить проблемы масштабируемости и удобства использования, не ставя под угрозу децентрализацию и используя существующее сообщество разработчиков и экосистему. Он направлен на улучшение существующих платформ путем обеспечения масштабирования и превосходного пользовательского опыта для dApps и функциональности пользователя.

Это решение для масштабирования публичных блокчейнов. Polygon PoS поддерживает все существующие инструменты Ethereum и предлагает более быстрые и дешевые транзакции.

## Ключевые особенности и основные моменты {#key-features-highlights}

- **Масштабируемость**: быстрые, недорогие и безопасные транзакции в сайдчейнах Polygon с финализацией, достигнутой в mainchain и Ethereum как первой совместимой базовой цепочке уровня 1.
- **Высокая пропускная способность**: достигнуто до 10 000 транзакций в секунду на единичном сайдчейне во внутренней тестовой сети. Планируется добавление нескольких цепочек для горизонтального масштабирования.
- **Пользовательский опыт**: плавный UX и абстрагирование разработчиков от mainchain к цепочке Polygon; нативные мобильные приложения и SDK с поддержкой WalletConnect.
- **Безопасность**: операторы сети Polygon сами являются владельцами стейка в системе PoS.
- **Публичные сайдчейны**: сайдчейны Polygon являются общедоступными по своей природе (в отличие от отдельных цепочек DApp), не имеют разрешений и могут поддерживать несколько протоколов.

Система Polygon была специально разработана для поддержки произвольных переходов состояний в сайдчейнах Polygon, которые поддерживают EVM.

## Роли делегат и валидатора {#delegator-and-validator-roles}

Вы можете участвовать в сети Polygon в качестве делегата или валидатора. См.

* [Кто такой валидатор](/docs/maintain/polygon-basics/who-is-validator)
* [Кто такой делегат](/docs/maintain/polygon-basics/who-is-delegator)

## Архитектура {#architecture}

Если ваша цель — стать валидатором, важно, чтобы вы понимали архитектуру Polygon.

Дополнительную информацию см. в разделе [«Архитектура Polygon»](/docs/maintain/validator/architecture).

### Компоненты {#components}

Чтобы получить детальное представление об архитектуре Polygon, ознакомьтесь с основными компонентами:

* [Heimdall](/docs/pos/heimdall/overview)
* [Bor](/docs/pos/bor/overview)
* [Контракты](/docs/pos/contracts/stakingmanager)

#### Кодовые базы {#codebases}

Чтобы иметь детальное представление об основных компонентах, см. следующие кодовые базы:

* [Heimdall](https://github.com/maticnetwork/heimdall)
* [Bor](https://github.com/maticnetwork/bor)
* [Контракты](https://github.com/maticnetwork/contracts)

## Инструкции {#how-tos}

### Настройка ноды {#node-setup}

Если вы хотите запустить полный узел в Polygon Mainnet или Mumbai Testnet, вы можете следовать Запустите руководство [в узел](/maintain/validate/run-validator.md) валидатора.

### Операции стейкинга {#staking-operations}

Проверьте, как осуществляется процесс стейкинга для профилей валидатора и делегата:

* [Операции стейкинга валидатора](docs/maintain/validate/validator-staking-operations)
* [Делегировать](/docs/maintain/delegate/delegate)
