# Hardhat ERC20

- Пройти [Lesson 12: Hardhat ERC20s](https://github.com/smartcontractkit/full-blockchain-solidity-course-js#lesson-12-hardhat-erc20s)

Критерии прохождения задания:
 - Изучить стандарт ERC20, разобрать все основные методы.
 - Написать простой ERC20 токен без использования OpenZeppelin.
 - Задеплоить свой токен в тестовую сеть, добавить этот токен в метамаск, потыкать его на etherscan.
 - Понять как работают `transfer`, `transferFrom` и `approve` и чем отличается перевод ERC20-токена от нативной валюты блокчейна (например, ETH).
 - Пройтись по литературе на которую приведены ссылки.

Дополнительно:

    * Необязательно делать если пока нет четкого понимания работы ERC20, но потом нужно вернуться.

 - Попробовать добавить все расширения и потыкать как это работает
 - Попробовать добавить Permit, сформировать и передать подпись в контракт.
 - Попробовать добавить transferAndCall.
        
## Какие навыки даст задание?

1. Понимание общего принципа ERC20 токена - несмотря на недостатки (которые частично закрываются расширениями) такой токен используется почти в каждом DeFi протоколе, поэтому важно знать как работают основные функции и для чего они нужны. Задание даст понимание базы, но в таком "чистом" виде ERC20 в природе почти не встречается, его всегда расширяют дополнительным функционалом, поэтому неплохо ознакомиться с подобными расширениями.
2. Понимание что такое EIP, ERC и как с ними работать.

## Вопросы по теории:

1. Что такое EIP? Что такое ERC? В чем отличие?
2. Какие три основных вида EIP существуют и что они в себя включают? Почему разработка и поддержка EIP сообществом ethereum это важно?
3. Каким по назначению может быть ERC20 токен? Что такое утилити токена?
4. Какие методы должны быть в токене ERC20? Что они делают? Какие обязательные, а какие нет?
5. Какие функции в смарт-контракте токена нужны для управления эмиссией?
6. Какая уязвимость связана с апрувом и какие способы защиты от подобных атак? Какие методы позволяют защитится от нее?
7. Зачем нужны хуки `_beforeTokenTransfer` и `_afterTokenTransfer`? Как их использовать, какие есть правила при использовании хуков? В каких методах ERC20 они могут быть?
8. Какие недостатки есть у ERC20?
9. Какие расширения ERC20 есть у OpenZeppelin?
10. Расширения ERC20, Какой функционал добавляют следующие расширения:
	- Burnable. 
	- Capped.
	- Pausable
	- Snapshot
	- Wrapper
11. Расширения, которые помогают устранить недостатки ERC20:
	- Permit (ERC2612). Какие варианты использования?
	- TransferAndCall (ERC-223, ERC-677, ERC-1363) В чем преимущества и недостатки трех подходов?
    - В чем отличие ERC777 от ERC20? Какие преимущества дает ERC777? Почему сообщество отказалось от идеи использовать ERC777?
	- Tokenized Vault Standard (ERC4626). Для чего нужен?
12. Утилиты
	- SafeTransfer - как использовать библиотеку и зачем? Какие есть аналоги?


### Литература помимо той, что дана в курсе:

- [Understand the ERC-20 token smart contract](https://ethereum.org/en/developers/tutorials/understand-the-erc-20-token-smart-contract/)
- [Набор контрактов и утилит ERC20 от OpenZeppelin](https://docs.openzeppelin.com/contracts/4.x/api/token/erc20#IERC20)
- [ERC20 Github OpenZeppelin](https://github.com/OpenZeppelin/openzeppelin-contracts/blob/master/contracts/token/ERC20/ERC20.sol)
- [Использование хуков ERC20](https://docs.openzeppelin.com/contracts/4.x/extending-contracts#using-hooks)
- [YouTube: ERC20 Token Tutorial](https://www.youtube.com/watch?v=gc7e90MHvl8)
- [Introduction To ERC Token Standards](https://medium.com/immunefi/how-erc-standards-work-part-1-c9795803f459)
- [EIPs](https://eips.ethereum.org/)
- [Tokenized Vault Standard](https://ethereum.org/en/developers/docs/standards/tokens/erc-4626/)
- [ERC-677](https://github.com/ethereum/EIPs/issues/677)
- [EIP-1363](https://eips.ethereum.org/EIPS/eip-1363)
- [Deprecate ERC777 implementation](https://github.com/OpenZeppelin/openzeppelin-contracts/issues/2620)
- [Deprecate ERC777 ethereum.org](https://ethereum.org/en/developers/docs/standards/tokens/erc-777/)