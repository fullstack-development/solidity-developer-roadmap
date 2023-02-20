
# Вопросы по Solidity

## Try / Catch
1. Что такое Try / Catch? Как эта конструкция используется в языке Solidity? Какие могут быть причины ошибки вызова функции смарт-контракта?
2. Какие типы блоков Catch поддерживаются в Solidity?
  - Какой тип блока catch используется для ```revert("reasonString")```?
  - Какой тип блока catch используется, если ошибка была вызвана делением на ноль?
  - Какие типы блока catch используется, если ошибка не подходит под два предыдущих случая, но ошибку необходимо обработать?
3. Чем отличается Try / Catch от других вариантов обработки ошибок(require, assert, revert)?
  - Может ли вызов функции через call заменить конструкцию Try / Catch?

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
