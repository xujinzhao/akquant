# 快速开始

在此处通过一个简单的例子来介绍如何使用 `pybroker` 来开发策略。

## 导入相关的模块和类

```python
import pybroker as pb
from pybroker import Strategy, StrategyConfig
from pybroker.ext.data import AKShare
```

1. 将 pybroker 模块导入为 `pb`，这是一个约定俗成的做法，方便后续使用。
2. 从 `pybroker` 中导入 `Strategy` 和 `StrategyConfig` 类，以及 `AKShare` 数据源。
3. `Strategy` 类是 pybroker 中的策略基类，所有的策略都需要继承该类。
4. `StrategyConfig` 类是 pybroker 中的策略配置基类，所有的策略配置都需要继承该类。
5. `AKShare` 类是 pybroker 中的数据源类，用于获取数据。

##  配置策略

```python
config = StrategyConfig(initial_cash=500_000)
```

1. 创建一个策略配置对象，该对象用于配置策略的一些参数。
2. `initial_cash` 参数用于配置策略的初始资金，默认为 10 万。

## 定义规则

```python
def buy_low(ctx):
    # If shares were already purchased and are currently being held, then return.
    if ctx.long_pos():
        return
    # If the latest close price is less than the previous day's low price,
    # then place a buy order.
    if ctx.bars >= 2 and ctx.close[-1] < ctx.low[-2]:
        # Buy a number of shares that is equal to 25% the portfolio.
        ctx.buy_shares = ctx.calc_target_shares(0.25)
        # Set the limit price of the order.
        ctx.buy_limit_price = ctx.close[-1] - 0.01
        # Hold the position for 3 bars before liquidating (in this case, 3 days).
        ctx.hold_bars = 3
```

1. 定义一个名为 `buy_low` 的函数，该函数用于判断是否需要买入。
2. `ctx` 参数是一个上下文对象，该对象包含了策略运行时的一些数据。
3. `ctx.long_pos()` 方法用于判断是否已经持有仓位。
4. `ctx.bars` 属性用于获取当前的交易日。
