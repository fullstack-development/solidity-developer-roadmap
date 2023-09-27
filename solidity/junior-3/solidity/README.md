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
5. Можно ли реализовать метатранзакции нативно?
   - Как работает следующий пример кода?
    ```solidity
        // SPDX-License-Identifier: UNLICENSED
        pragma solidity ^0.8.19;

        import "@openzeppelin/contracts/token/ERC20/ERC20.sol";

        contract Token is ERC20 {
            bytes32 public constant META_TRANSACTION_TYPEHASH =
                keccak256("MetaTransaction(uint256 nonce,address signer,bytes functionSignature)");

            mapping(address signer => uint256 nonce) private _nonces;

            struct MetaTransaction {
                uint256 nonce;
                address signer;
                bytes functionSignature;
            }

            event MetaTransactionExecuted(
                address signer,
                address relayer,
                bytes functionSignature
            );

            error ZeroAddress();
            error InvalidSignature();
            error InvalidCall();

            constructor() ERC20("Token", "MTT") {}

            function DOMAIN_SEPARATOR() public view returns (bytes32) {
                return keccak256(
                    abi.encode(
                        keccak256("EIP712Domain(string name,string version,uint256 chainId,address verifyingContract)"),
                        keccak256("EIP712"),
                        keccak256("1"),
                        block.chainid,
                        address(this)
                    )
                );
            }

            function executeMetaTransaction(
                address signer,
                bytes memory functionSignature,
                uint8 v,
                bytes32 r,
                bytes32 s
            ) external payable returns (bytes memory result) {
                MetaTransaction memory _tx = MetaTransaction({
                    nonce: _nonces[signer],
                    signer: signer,
                    functionSignature: functionSignature
                });

                bool isVerify = _verify(signer, _tx, v, r, s);
                if (!isVerify) {
                    revert InvalidSignature();
                }

                _nonces[signer] += 1;

                (bool success, bytes memory data) = address(this).call(
                    abi.encodePacked(functionSignature, signer)
                );

                if (!success) {
                    revert InvalidCall();
                }

                emit MetaTransactionExecuted(signer, msg.sender, functionSignature);

                return data;
            }

            function getNonce(address account) external view returns (uint256) {
                return _nonces[account];
            }

            function _msgSender() internal view override returns (address sender) {
                if (msg.sender == address(this)) {
                    assembly {
                        sender := shr(96, calldataload(sub(calldatasize(), 20)))
                    }
                }
                else {
                    return super._msgSender();
                }
            }

            function _verify(
                address signer,
                MetaTransaction memory _tx,
                uint8 v,
                bytes32 r,
                bytes32 s
            ) private view returns (bool) {
                if (signer == address(0)) {
                    revert ZeroAddress();
                }

                return signer == ecrecover(_getDigest(_tx), v, r, s);
            }

            function _getDigest(MetaTransaction memory _tx) private view returns (bytes32) {
                return keccak256(
                    abi.encodePacked(
                        "\x19\x01",
                        DOMAIN_SEPARATOR(),
                        keccak256(
                            abi.encode(
                                META_TRANSACTION_TYPEHASH,
                                _tx.nonce,
                                _tx.signer,
                                keccak256(_tx.functionSignature)
                            )
                        )
                    )
                );
            }
        }
    ```
6. Творческий вопрос. Как ты считаешь, на сколько важны метатранзакции? Есть ли у них будущее? Нарушают ли они какие-нибудь законы децентрализации?

- [Gas-free transactions: Meta Transactions explained](https://medium.com/coinmonks/gas-free-transactions-meta-transactions-explained-f829509a462d)
- [ERC-2771](https://eips.ethereum.org/EIPS/eip-2771)
- [Gas Station Network](https://docs.opengsn.org/)
- [Native Meta Transactions](https://medium.com/gitcoin/native-meta-transactions-e509d91a8482)

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

## Bitwise operators

1. Что такое бит и байт, в чем отличие?
2. Что такое знаковые и беззнаковые числа в контексте битов?
3. Какие бывают виды знаковых чисел? Какой вид самый используемый?
4. Как работают прямой, обратный и дополнительный код? Какие проблемы могут возникнуть в прямом и обратном коде?
5. Что такое битовые операции?
6. Какие существуют битовые операции?
7. Что такое логические вентили?
8. Какие действия можно выполнять с битами используя битовые операции?
9. Что такое битовые сдвиги?
10. Как работают арифметический, логический и циклический сдвиги? В чем отличия?
11. Где используются битовые операции и для чего?
12. Что происходит в этом коде? Как можно сделать то же самое по-другому?
```js
    function bitOperation(uint8 number, uint8 index) external pure returns (uint256) {
        return number & ~(1 << index);
    }
```

-   [Двоичные числа](https://asm.kcup.tusur.ru/Library/chapter%201/1-1.html)
-   [Как два байта переслать](https://pikabu.ru/story/kak_dva_bayta_pereslat_7070913)
-   [Прямой, обратный и дополнительный код](https://microkontroller.ru/programmirovanie-mikrokontrollerov-avr/pryamoy-obratnyiy-dopolnitelnyiy-kod-dvoichnogo-chisla/)
-   [Видео: как работают отрицательные числа](https://www.youtube.com/watch?v=BIYiuy8WWiU)
-   [Bitwise operation](https://en.wikipedia.org/wiki/Bitwise_operation)
-   [Видео: как работать с битами](https://www.youtube.com/watch?v=qewavPO6jcA)
-   [Побитовые операции](https://neerc.ifmo.ru/wiki/index.php?title=%D0%9F%D0%BE%D0%B1%D0%B8%D1%82%D0%BE%D0%B2%D1%8B%D0%B5_%D0%BE%D0%BF%D0%B5%D1%80%D0%B0%D1%86%D0%B8%D0%B8)