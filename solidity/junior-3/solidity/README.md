# Вопросы по Solidity

## Digital signatures

1. Что такое цифровая подпись? Для чего используется подпись?
    - В чем разница между подписью транзакции и подписью произвольного сообщения?
2. Что такое ECDSA в общих чертах(глубокое математическое понимание не нужно)?
    - Что понимается под обозначением {**r**, **s**, **v**}? Как называется и что решает {**v**}?
3. В кошельках подпись часто используется в следующем виде:
  ```0x0f1928d8f26b2d9260929425bdc6ac922f7d787fd73b42afe2548776a0e858016f52826d8ab67e1c84e6e6778fa4769d8aa4f014bf76b3280be77e4e0c447f9b1c```
  Как из этого получить {**r**, **s**, **v**}?
4. Что можно рассказать про следующие стандарты по работе с подписями?
    - Personal_sign. Как гарантируется, что эта подпись может быть использована только в Ethereum сети?
    - EIP-191: Signed Data Standard. Для чего используется **0x19**?
    - EIP-712: Ethereum typed structured data hashing and signing. Что решает Domain? Что решает hashStruct?
1. Как на контракте проверить подпись?
    - Что такое ```ecrecover()```?
    - Что предлагает библиотека OpenZeppelin?
2. Приведи три примера того, как можно использовать цифровую подпись.

- [Digital signatures](https://ethereum.org/en/glossary/#digital-signatures)
- [The Magic of Digital Signatures on Ethereum](https://medium.com/mycrypto/the-magic-of-digital-signatures-on-ethereum-98fe184dc9c7)
- [Intro to Cryptography and Signatures in Ethereum](https://medium.com/immunefi/intro-to-cryptography-and-signatures-in-ethereum-2025b6a4a33d)
- [Математические и криптографические функции](https://docs.soliditylang.org/en/v0.8.19/units-and-global-variables.html#mathematical-and-cryptographic-functions)
- [EIP-191](https://eips.ethereum.org/EIPS/eip-191)
- [Testing EIP-712 Signatures](https://book.getfoundry.sh/tutorials/testing-eip712)

## Meta transactions

1. Что такое метатранзакции?
2. Для чего можно применять метатранзакции? Назвать не менее трех вариантов использования.
3. Какая основная идея стандарта ERC-2771?
    - Какая задача отводится контракту **Forwarder**?
    - Для чего необходимо использовать ```_msgSender()``` вместо ```msg.sender```?
4. Gas Station Network - это пример проекта с открытым исходным кодом, который помогает реализовать метатранзакции. Можешь рассказать, как он устроен, как работает, его верхнеуровневую архитектуру?
    - Для чего необходимо реализовать контракт ```Paymaster```?
    - Можно ли использовать [контракты из библиотеки OpenZeppelin](https://docs.openzeppelin.com/contracts/4.x/api/metatx) для организации метатранзакций?
    - Какие еще есть сервисы, которые можно использовать для организации метатранзакций?
5. Творческий вопрос. Как ты считаешь, на сколько важны метатранзакции? Есть ли у них будущее? Нарушают ли они какие-нибудь законы децентрализации?

- [Gas-free transactions: Meta Transactions explained](https://medium.com/coinmonks/gas-free-transactions-meta-transactions-explained-f829509a462d)
- [ERC-2771](https://eips.ethereum.org/EIPS/eip-2771)
- [Gas Station Network](https://docs.opengsn.org/)

## Oracles

1. Что такое оракул?
    - Для чего нужны оракулы?
2. Как технически можно организовать работу оракула? (Желательно подготовить схему работы для объяснения)
    - Сколько смарт-контрактов необходимо?
    - Какие предъявляются требования к off-chain части оракула?
    - Есть ли затраты на использование оракула и кто оплачивает эти расходы?
3. Мы подготовили несколько вариантов классификации оракулов. Расскажи, как ты понимаешь такое разбиение? Согласен ли ты с ним?
    - Централизованные vs децентрализованные?
    - Immediate read oracles vs publish-subscribe oracles vs request-response oracles?
4. Одним из самых популярных сервисов среди оракулов является chainlink. Что можешь рассказать про него?
    - Какую роль в экосистеме играет токен Link?
    - Что такое "Basic request model"?
    - Что такое "Off-Chain Reporting"?
    - Как работают price feeds?
    - Что такое VRF?
    - Для чего используются Keepers?
5. Творческий вопрос. Как ты считаешь оракулы это больше про "возможности" или "опасности"? Это безопасный способ взаимодействия смарт-контрактов с внешним миром или это потенциально узкое место, которое вредит децентрализации и к тому же подобное решение легко взломать? Здесь нужно рассказать собственное отношение к оракулам.

- [WHY DO SMART CONTRACTS NEED ORACLES?](https://ethereum.org/en/developers/docs/oracles/#why-do-smart-contracts-need-oracles)
- [Oracles](https://ethereum.org/en/developers/docs/oracles/)
- [Implementing a Blockchain Oracle on Ethereum](https://medium.com/@pedrodc/implementing-a-blockchain-oracle-on-ethereum-cedc7e26b49e)
- [Chainlink](https://chain.link/)

## Evm opcodes

1. Что такое opcodes?
    - Что означает цепочка ```Solidity → Байт-код → Opcodes```?
    - Для чего необходимо базовое понимание opcodes?
2. Известно, что opcodes условно делятся на несколько групп. Твоя задача на каждую группу привести в пример несколько opcodes и обозначить предназначение всей группы.
    - Управление стеком.
    - Арифметика
    - Операции среды
    - Управление памятью memory
    - Управление памятью storage
    - Управление program counter
    - Остановка процесса
3. За выполнение каждого opcode, требуется оплата за выполнение в сети. Оплата выражена в единицах, которые называются газ.
    - В чем разница между базовой стоимостью выполнения opcode и динамической?
    - Какой самый дорогой opcode? Сколько газа он требует?
4. Что делает следующий байт-код? Какой будет результат выполнения?
   > 6002600404600201

- [Evm opcodes](https://www.evm.codes/?fork=shanghai)
- [The Ethereum Virtual Machine — How does it work?](https://medium.com/mycrypto/the-ethereum-virtual-machine-how-does-it-work-9abac2b7c9e)