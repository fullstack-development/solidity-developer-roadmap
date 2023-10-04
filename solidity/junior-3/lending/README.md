# Вопросы по lending протоколам

## Общие вопросы

1. Что такое lending протоколы? Для чего используются?
2. Чем borrower отличается от lender?
4. Что такое collateral в рамках lending протоколов? Для чего используется?
5. Что такое interest rates? Для чего используется?
6. Почему заем требует обеспечение?
7. Что такое ликвидация? Для чего нужна? Какие виды ликвидаций бывают? Что такое каскадные ликвидации?
8. В разных протоколах бывают разные параметры, которые регулируют процесс ликвидации, например "health factor" в Aave. Как ты понимаешь его работу?

## Вопросы по протоколам

### Compound V2

1. Что такое market? Что означает термин выйти на рынок (enter market)?
2. Для чего используется контракт [cToken](https://github.com/compound-finance/compound-protocol/blob/master/contracts/CToken.sol)?
3. Для чего используется контракт [Comptroller](https://github.com/compound-finance/compound-protocol/blob/master/contracts/Comptroller.sol)?
4. Расскажи про каждую из этих процентных ставок протокола:
    - exchange rate
    - supply rate
    - borrow rate.
5. Как работает начисление процентов в протоколе compound?
6. Что означает термин utilization rate?
7. Для чего используется параметр kink?
8. Для чего нужен токен COMP?

### Aave v2

1. Что такое [AToken](https://github.com/aave/protocol-v2/blob/master/contracts/protocol/tokenization/AToken.sol) и debtToken? Какие виды debtToken существуют?
2. Для чего используется контракт [LendingPool](https://github.com/aave/protocol-v2/blob/master/contracts/protocol/lendingpool/LendingPool.sol)?
3. Что такое health factor?
4. Что такое collateral swap?
5. Что такое native credit delegation?
6. Как работают flexible rates?
7. Что такое flash loans? Для чего используются? Как работают? Как ты думаешь, технология несет больше вреда или пользы?
8. Для чего нужен токен AAVE?

## Стейблкоины

1. Что такое стейблкоин? В чем его отличие от обычного токена? Какие стейблкоины знаешь?
2. Чем централизованные стейблкоины отличаются от децентрализованных? Можно ли централизацию замаскировать в децентрализованном стейблкоине? Например блокировать транзакции, вносить адреса в черный список и так далее.
3. Стейблкоины бывают разной степени обеспеченности (частично обеспеченные, полностью обеспеченные, сверх обеспеченные). Для чего это нужно?
4. Что такое алгоритмические стейблкоины? В чем отличие моделей привязки ребейз, сеньораж и фракционной друг от друга?
5. По какой причине стейблкоин может потерять привязку?
6. Что общего между стейблкоином и lending протоколом?

## Links

1. [Compound](https://compound.finance/)
2. [Aave](https://aave.com/)
3. [Видео](https://www.youtube.com/watch?v=wUjYK5gwNZs&list=PL4Rj_WH6yLgWe7TxankiqkrkVKXIwOP42&index=3&ab_channel=PatrickCollins) про стейблкоин от Patrick Collins из chainlink. Урок 12.
4. [What are Decentralized Stablecoins? A Look At DAI, GHO, crvUSD, FRAX, and More](https://www.coingecko.com/learn/what-are-decentralized-stablecoins#4)
5. [Stability, Elasticity, and Reflexivity: A Deep Dive into Algorithmic Stablecoins](https://insights.deribit.com/market-research/stability-elasticity-and-reflexivity-a-deep-dive-into-algorithmic-stablecoins/)