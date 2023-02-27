
# Вопросы по Solidity

## Function selector

1. Что такое сигнатура функции? Что такое селектор функций и как он создается в Solidity? Какие есть способы получить селектор функции в смарт-контракте? (назвать несколько)
2. Как селекторы функций связаны с ABI (Application Binary Interface) в Solidity и какое значение имеет ABI для разработки контрактов?
3. Можете ли быть так, что две функции в контракте Solidity могут иметь одинаковое имя, но разные селекторы функций?
4. Отличаются ли вычисление селекторов функций в разных версиях Solidity? Как обеспечить совместимость между разными версиями Solidity?
5. Как можно использовать селекторы функций для оптимизации использования газа в контрактах Solidity?

- [Solidity docs](https://docs.soliditylang.org/en/develop/abi-spec.html#function-selector)
- [A technical primer on using encoded function calls](https://medium.com/linum-labs/a-technical-primer-on-using-encoded-function-calls-50e2b9939223)
- [How To Decipher A Smart Contract Method Call](https://medium.com/@hayeah/how-to-decipher-a-smart-contract-method-call-8ee980311603)
- [Advanced gas optimization tips for Solidity](https://coinsbench.com/advanced-gas-optimizations-tips-for-solidity-85c47f413dc5#:~:text=to%20gas%20specifications.-,Function%20names,-Solidity%20compiler%20reads)

## Upgradeable контракты
1. Что такое обновляемые контракты? Для чего это нужно?
2. Можно ли мигрировать данные с одного смарт-контракта на другой?
  - Как это сделать?
  - Что мешает это сделать или в чем основная сложность?
3. Может ли помочь в обновление кода контрактов разделение хранения данных и логики реализации по разным контрактам?
4. Можно ли применять поведенческие шаблоны проектирования для разделения хранения данных и логики? Как применить шаблон Strategy?
  - Можно ли при использование паттерна Strategy обновить главный контракт логики?
5. Как применить шаблон проектирования Proxy для обновления контрактов?
  - Как работает прокси для смарт-контрактов? В чем основной концепт? Как в этом концепте участвует функция ```delegateCall()```?
  - Что такое конфликт селекторов функций?
  - Для чего нужен стандарт ERC-1967: Proxy Storage Slots?
  - Что можно рассказать про Transparent proxy? Как он устроен? Для чего предназначался?
  - Что такое UUPS? В чем его отличие от Transparent?
  - Для чего был придуман Beacon Proxy?
  - Что такое EIP-1167? Для чего библиотека Clones от OpenZeppelin? Можно ли обновлять прокси, созданные при помощи этой библиотеки?
6. В чем основная идея Diamond Proxy? Для каких случаеа предназачался этот подход?
  - В чем отличие Inherited storage VS Diamond Storage VS App Storage?
7. В чем плюсы и минусы использования обновляемых контрактов?
