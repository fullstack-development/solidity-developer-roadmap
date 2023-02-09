# Комментирование кода

> Все слышали выражение: "Хороший код не нуждается в комментариях". Это неоспоримая истина и ложь одновременно.

Согласно [официальной документации](https://docs.soliditylang.org/en/v0.8.18/natspec-format.html) в Solidity можно использовать специальную форму написания комментариев. Эта специальная форма называется Ethereum Natural Language Specification Format (NatSpec).

Основным ориентиром при создание NatSpec был [Doxygen](https://www.doxygen.nl/).

_Важно!_ Рекомендуется, чтобы контракты Solidity были полностью аннотированы с использованием NatSpec для всех общедоступных интерфейсов (все что будет определено в ABI)

## Автогенерация документации

На основе комментариев можно сгенерировать документацию для смарт-контрактов при помощи:
1. [Компилятор Solidity](https://docs.soliditylang.org/en/v0.8.18/natspec-format.html#documentation-output).
2. [Решение от OpenZeppelin](https://github.com/OpenZeppelin/solidity-docgen) по генерации документации.
