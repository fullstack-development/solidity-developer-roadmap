# Linting and Formatting

Для того чтобы писать чистый и понятный другим разработчикам команды код обычно используют два вида инструментов: линтеры и форматеры.

**Линтеры** автоматически анализируют код на наличие возможных программных ошибок и ошибок стиля.

**Форматеры** автоматически форматируют код в соответствии с предопределенными правилами и значениями отступов по умолчанию.

Язык Solidity не является исключением. Мы предлагаем обратить внимание на следующие инструменты, которые позволят автоматизировать рабочий процесс написания кода в команде.

_Важно!_ Для того чтобы начать писать смарт-контракты на Solidity не обязательно сразу глубоко уметь разбираться во всех инструментах для линтинга и форматирования кода. Но важно знать, какие есть инструменты и для чего они используются. И когда в ходе разработки ты почувствуешь необходимость в использование какого-то из этих инструментов, ты уже будешь знать, что тебе нужно использовать.

## Linters

- [Solhint](https://www.npmjs.com/package/solhint). Самый популярный линтер.
- [Ethlint](https://www.npmjs.com/package/ethlint). Раньше этот инструмент назывался Solium.

## Formatters

 - [Prettier solidity](https://github.com/prettier-solidity/prettier-plugin-solidity). Работает в связке с solhint.

## Git hooks

  Про то что такое, git hooks можно почитать [тут](https://githooks.com/)

 - [Husky](https://github.com/typicode/husky). Этот инструмент может запускать линтер и форматер перед каждым **commit**, **push** или **receive**.

## Расширения для vscode

### Общие расширения
- [Поддержка языка Solidity](https://juan.blanco.ws/solidity-contracts-in-visual-studio-code/).
- [Solidity Visual Developer](https://marketplace.visualstudio.com/items?itemName=tintinweb.solidity-visual-auditor).
- [Solidity+Yul Semantic Syntax](https://marketplace.visualstudio.com/items?itemName=ContractShark.solidity-lang)

### HardHat
- [Поддержка языка Solidity и интеграция Hardhat](https://marketplace.visualstudio.com/items?itemName=NomicFoundation.hardhat-solidity).
- [Mocha Test Explorer](https://marketplace.visualstudio.com/items?itemName=hbenl.vscode-mocha-test-adapter)

### Foundry
- [Coverage Gutters](https://marketplace.visualstudio.com/items?itemName=ryanluker.vscode-coverage-gutters)
- [Forge Snippets](https://marketplace.visualstudio.com/items?itemName=Crisgarner.foundry-snippets)
- [Foundry Test Explorer](https://marketplace.visualstudio.com/items?itemName=naps62.foundry-vscode-test-adapter)
- [TOML language support](https://marketplace.visualstudio.com/items?itemName=be5invis.toml)

_Важно!_ Нужно быть внимательным. Расширения для поддержки языка могут конфликтовать друг с другом. Не обязательно использовать все расширения сразу.

Список интеграций для других IDE можно посмотреть [тут](https://docs.soliditylang.org/en/v0.8.18/resources.html#editor-integrations).

## Linting and formatting для тестов

Есть несколько подходов в организации тестов для смарт контрактов. Например, для Foundry тесты пишутся на языке Solidity и это значит, что нам достаточно стандартного линтинга и форматирования только для языка Solidity.

В других средах разработки ситуация может быть немного иной. Например в Hardhat используются: библиотека [ethers.js](https://docs.ethers.org/v5/) и тестовый фреимворк [mocha](https://mochajs.org/). Это подразумевает написание тестов на языке [javascript](https://learn.javascript.ru/) или [typescript](https://www.typescriptlang.org/).

- [ESLint](https://eslint.org/). Понадобится для линтинга js или ts.

_Важно!_ Для других фреймворков могут понадобиться свои инструменты линтинга и форматирования.
