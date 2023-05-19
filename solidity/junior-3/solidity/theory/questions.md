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
