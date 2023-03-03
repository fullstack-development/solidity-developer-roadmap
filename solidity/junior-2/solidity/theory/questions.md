
# Вопросы по Solidity

## Call, staticcall, delegatecall, сalling other сontract

1. Для чего нужна низкоуровневая функция `call`, какие аргументы принимает?
2. Что возвращает функция `call`? Как декодировать возвращаемые значения?
3. Почему метод передачи эфира через `call` является предпочтительным?
4. Можно ли указывать лимит газа для транзакции при вызове `call`? Если да, то зачем указывать лимит газа и какие могут быть проблемы?
5. Для чего нужна низкоуровневая функция `staticcall`, в чем отличие от `call`?
6. Для чего нужна низкоуровневая функция `delegatecall`, в чем отличие от `call` и `staticcall`?
7. Какие возможны уязвимости связанные с `delegatecall`?
8. Как все эти функции связаны с `msg.value` и `msg.data`?
9. Как вызвать другой контракт с помощью этих функций? Как вызвать конкретную функцию другого контракта с аргументами?
10. По каким причинам низкоуровневый вызов других смарт-контрактов через `call` не является предпочтительным?
11. Приведи несколько примеров, когда без низкоуровневого вызова другого смарт-контракта через `call` и `delegatecall` не обойтись?

- [Solidity docs: ](https://docs.soliditylang.org/en/v0.8.19/introduction-to-smart-contracts.html#message-calls)
- [Solidity docs: Members of Address Types](https://docs.soliditylang.org/en/v0.8.11/units-and-global-variables.html#members-of-address-types)
- [Learn Solidity lesson 34. Call, staticcall and delegatecall](https://medium.com/coinmonks/call-staticcall-and-delegatecall-1f0e1853340)
- [Solidity by example - Call](https://solidity-by-example.org/call/)
- [SWC-112 - delegatecall](https://swcregistry.io/docs/SWC-112)

## Try / Catch

1. Что такое Try / Catch? Как эта конструкция используется в языке Solidity? Какие могут быть причины ошибки вызова функции смарт-контракта?
2. Какие типы блоков Catch поддерживаются в Solidity?
  - Какой тип блока catch используется для ```revert("reasonString")```?
  - Какой тип блока catch используется, если ошибка была вызвана делением на ноль?
  - Какие типы блока catch используется, если ошибка не подходит под два предыдущих случая, но ошибку необходимо обработать?
3. Чем отличается Try / Catch от других вариантов обработки ошибок(require, assert, revert)?
4. Может ли вызов функции через call заменить конструкцию Try / Catch?

- [Solidity docs](https://docs.soliditylang.org/en/v0.8.19/control-structures.html#try-catch)

## Import

1. Идея ```import``` основана на **коцепции модулей**. В чем основная суть этого концепта?
2. Local **vs** external. В чем разница?
3. **Specific import**. Как этим пользоваться?
  - Нужно ли стремиться использовать **specific import** за место импорта всего, что есть в файле? Например, ```import "./Storage.sol"```
  - Что можно импортировать из файла ```Storage.sol``` для использования в контракте ```SpecificImport```?

  ```solidity
    /// SpecificImport.sol

    // SPDX-License-Identifier: MIT

    pragma solidity 0.8.17;

    import {
        // Что можно импортировать из контракта Storage?
    } from "./Storage.sol";

    contract SpecificImport {}
  ```

  ```solidity
    /// Storage.sol

    // SPDX-License-Identifier: MIT

    pragma solidity 0.8.17;

    address constant OWNER = 0x607B5e673D3ea42A0F85aDD6f529196500FC9E04;
    uint256 constant STORAGE_SLOT = 113;

    struct StorageList {
        address storageContract;
    }

    interface IStorage {
        function getStorageSlot() external view returns (uint256);
        function setStorageSlot(uint256 newStorageSlot) external;
    }

    library Array {
        function removeItem(uint256 index) external {}
    }

    enum STATUS {
        ACTIVE,
        PAUSED
    }

    error Storage_SetStorageLimit();

    // User-defined value type. More https://docs.soliditylang.org/en/v0.8.13/types.html#user-defined-value-types
    type UFixed256x18 is uint256;

    contract Storage {
        uint256 private _storageSlot = STORAGE_SLOT;
        uint256 _maxSetStorageCount;

        mapping(address => uint256) _counter;

        event StorageSlotUpdated(address sender);

        constructor(uint256 maxSetStorageCount) {
            _maxSetStorageCount = maxSetStorageCount;
        }

        function getStorageSlot() external view returns (uint256) {
            return _storageSlot;
        }

        function setStorageSlot(uint256 newStorageSlot) external {
            if (_counter[msg.sender] >= _maxSetStorageCount) {
                revert Storage_SetStorageLimit();
            }

            _storageSlot = newStorageSlot;

            _counter[msg.sender] += _counter[msg.sender];

            emit StorageSlotUpdated(msg.sender);
        }
    }

    function createStorage(uint256 maxSetStorageCount) returns (address)  {
        Storage storageImpl = new Storage(maxSetStorageCount);
        return address(storageImpl);
    }

   ```
4. **Import Aliases**. Ключевое слово **as**. Для чего это нужно?

- [Solidity docs](https://docs.soliditylang.org/en/v0.8.19/layout-of-source-files.html#importing-other-source-files)

## Library

1. Общие вопросы по библиотекам?
  - Можно ли отправить эфир библиотеке?
  - Есть ли в библиотеке переменные состояния?
  - Могут ли библиотеки содержать в себе ```receive()```, ```callback()``` или ```payable``` функции?
  - Могут ли библиотеки быть уничтожены через вызов ```selfdestruct()```?
  - Можно ли наследовать библиотеку и быть унаследованным?
2. Почему использование библиотеки дешевле, чем наследование контрактов?
3. Какие из перечисленных типов данных можно реализовать в библиотеке?
  - struct
  - enum
  - интерфейс
  - любую публичную переменную ```uint256 public myVar = 100;```
  - константу ```uint256 constant MY_CONSTANT = 100;```
  - модификатор
4. Какие есть варианты развертывания библиотеки? В чем разница между этими вариантами?
5. Можно ли объявлять в библиотеках функции без имплементации, как в интерфейсах?
  ```solidity
  function onConnect() public pure returns (bool);
  ```
6. Можно ли использовать ```Event``` в библиотеках? Могут ли возникнуть какие-то сложности в связи с этим?
7. Можно ли использовать модификаторы внутри библиотеки? Какие есть особенности с этим связанные?

- [Solidity docs](https://docs.soliditylang.org/en/v0.8.19/contracts.html#libraries)
- [Solidity Tutorial: all about Libraries](https://jeancvllr.medium.com/solidity-tutorial-all-about-libraries-762e5a3692f9)

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
