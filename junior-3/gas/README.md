# Вопросы про gas в EVM

## Общие вопросы

1. Что представляет из себя газ в контексте блокчейна?
2. Почему газ необходим EVM? Привести ключевые аспекты.

## Вопросы по gas price

1. В чем оплачивается комиссия за газ в Ethereum?
2. Кто устанавливает цены на газ в Ethereum?
3. За что отвечают параметры `gasPrice` и `gasLimit` в транзакции?
4. Как происходит расчет стоимости газа перед выполнением транзакции и что случается после ее завершения?
5. Какова формула для расчета комиссии за транзакцию в Ethereum 1.0 (до EIP-1559)?
6. По какому принципу майнеры отбирали транзакции в Ethereum 1.0?
7. Какие основные недостатки расчета газа были в Ethereum 1.0?
8. Как изменились параметры транзакции связанные с газом после EIP-1559? Рассказать про каждый из них.
9. Как изменилась модель расчета газа после внедрения EIP-1559? Как стала выглядеть формула расчета?
10. Что такое `base fee`? Кто его определяет и как он изменяется во времени?
11. Как `base fee` влияет на размер блока? Что происходит с `base fee` после выполнения транзакции?
12. От чего зависит скорость включения транзакции в блок Ethereum?
13. Возможно ли установить нулевые значения для `gasLimit`, `maxFeePerGas` или `maxPriorityFee`? Каковы будут последствия в каждом случае?
14. Какие типы транзакций существуют в Ethereum и в чем их отличия?

## Вопросы по gas used

1. За что отвечает параметр `gasUsed` в транзакции EVM и может ли он превышать `gasLimit`?
2. На что тратиться газ внутри EVM?
3. Когда возникает ошибка "out of gas"?
4. В каких ситуациях неиспользованный газ возвращается при возникновении ошибки EVM и когда нет?
5. Какие функции клиента go-ethereum ответственны за обработку транзакций и выполнение кода смарт-контрактов?
6. В чем различие между выполнением транзакции с вызовом смарт-контракта и без него?
7. Что такое статический и динамический газ в контексте EVM и как они рассчитываются?
8. Могут ли у операции в EVM отсутствовать затраты на динамический газ?
9. Как рассчитывается газ при работе с `memory`?
10. Какова роль значений `original`, `current` и `new` при записи данных в хранилище смарт-контракта?
11. Описать статусы хранилища (storage): "Dirty", "Fresh" и "No-op".
12. Для чего нужен был хард-форк St.Petersburg?
13. Что представляют собой "теплые" и "холодные" доступы к слотам хранилища?
14. Что такое списки доступа, как они работают и зачем они нужны?
15. Зачем нужен механизм возврата газа при очистке хранилища и в каких случаях он может быть полезен?
16. Что такое внутренний газ (intrinsic gas) транзакции и из чего он складывается?
    - Как считается газ за `calldata`?
    - Какой G-параметр учитывается в каждой транзакции?
17. Как происходит учет газа на уровне блока?
18. Как выглядит процесс учета газа на уровне транзакции?

## Links

-   [EIP-1559: Fee market change for ETH 1.0 chain](https://eips.ethereum.org/EIPS/eip-1559)
-   [Doc: Ethereum Whitepaper](https://ethereum.org/en/whitepaper#fees)
-   [Doc: Ethereum Yellow Paper](https://ethereum.github.io/yellowpaper/paper.pdf)
-   [Article: How does Ethereum work](https://www.preethikasireddy.com/post/how-does-ethereum-work-anyway)
-   [Article: Understanding the Ethereum virtual machine – part I](https://leftasexercise.com/2021/09/12/understanding-the-ethereum-virtual-machine-part-i/)
-   [Article: Understanding the Ethereum virtual machine – part II](https://leftasexercise.com/2021/09/15/understanding-the-ethereum-virtual-machine-part-ii/)
-   [Article: Understanding the Ethereum virtual machine – part III](https://leftasexercise.com/2021/09/19/q-understanding-the-ethereum-virtual-machine-part-iii/)
-   [Article: Dissecting EVM using go-ethereum Eth client implementation. Part III — bytecode interpreter](https://medium.com/@deliriusz/dissecting-evm-using-go-ethereum-eth-client-implementation-part-iii-bytecode-interpreter-8f144004ed7a)
-   [Article: EIP-2930 - Ethereum access list](https://www.rareskills.io/post/eip-2930-optional-access-list-ethereum)
-   [Code: Go-Ethereum](https://github.com/ethereum/go-ethereum)
