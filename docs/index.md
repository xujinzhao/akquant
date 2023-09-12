# PyBroker 介绍

> 你是否希望借助 Python 和机器学习的力量来优化您的交易策略？
> 那么你需要了解一下 PyBroker！这个 Python 框架专为开发算法交易策略而设计，
> 尤其关注使用机器学习的策略。借助 PyBroker，你可以轻松创建和微调交易规则，
> 构建强大的模型，并深入了解你的策略表现。

配置文档：[点击进入](https://squidfunk.github.io/mkdocs-material/)

PyBroker 项目 [GitHub 地址](https://github.com/edtechre/pybroker)

PyBroker 英文文档地址：[点击进入英文文档](https://www.pybroker.com/en/latest/)

PyBroker 中文文档地址：[点击进入中文文档](https://www.pybroker.com/zh_CN/latest/)

## 安装

```shell
pip install lib-pybroker --upgrade
```

## 环境配置

PyBroker 支持在 Windows、macOS 和 Linux 中
Python 3.9 及以上版本，建议使用 Python 3.11 及以上版本。

## 策略示例

``` py title="demo.py" linenums="1" hl_lines="2 7"
# 导入所需的库和模块
import pybroker as pb
from pybroker import Strategy, ExecContext
from pybroker.ext.data import AKShare

# 定义全局参数 "stock_code"（股票代码）、"percent"（持仓百分比）和 "stop_profit_pct"（止盈百分比）
pb.param(name='stock_code', value='600000')
pb.param(name='percent', value=1)
pb.param(name='stop_loss_pct', value=10)
pb.param(name='stop_profit_pct', value=10)

# 初始化 AKShare 数据源
akshare = AKShare()

# 使用 AKShare 数据源查询特定股票（由 "stock_code" 参数指定）在指定日期范围内的数据
df = akshare.query(symbols=[pb.param(name='stock_code')], start_date='20200131', end_date='20230228')


# 定义交易策略：如果当前没有持有该股票，则买入股票，并设置止盈点位
def buy_with_stop_loss(ctx: ExecContext):
    pos = ctx.long_pos()
    if not pos:
        # 计算目标股票数量，根据 "percent" 参数确定应购买的股票数量
        ctx.buy_shares = ctx.calc_target_shares(pb.param(name='percent'))
        ctx.hold_bars = 100
    else:
        ctx.sell_shares = pos.shares
        # 设置止盈点位，根据 "stop_profit_pct" 参数确定止盈点位
        ctx.stop_profit_pct = pb.param(name='stop_profit_pct')


# 创建策略配置，初始资金为 500000
my_config = pb.StrategyConfig(initial_cash=500000)
# 使用配置、数据源、起始日期、结束日期，以及刚才定义的交易策略创建策略对象
strategy = Strategy(akshare, start_date='20200131', end_date='20230228', config=my_config)
# 添加执行策略，设置股票代码和要执行的函数
strategy.add_execution(fn=buy_with_stop_loss, symbols=[pb.param(name='stock_code')])
# 执行回测，并打印出回测结果的度量值（四舍五入到小数点后四位）
result = strategy.backtest()
print(result.metrics_df.round(4))
```

``` shell title="shell" linenums="1" hl_lines="2 7"
Loading bar data...
Loaded bar data: 0:00:00 
Backtesting: 2020-01-31 00:00:00 to 2023-02-28 00:00:00
Loading bar data...
Loaded bar data: 0:00:00 
Test split: 2020-02-03 00:00:00 to 2023-02-28 00:00:00
100% (748 of 748) |######################| Elapsed Time: 0:00:00 Time:  0:00:00
Finished backtest: 0:00:03
                      name        value
0              trade_count     373.0000
1     initial_market_value  500000.0000
2         end_market_value  467328.0900
3                total_pnl  -33322.7800
4           unrealized_pnl     650.8700
5         total_return_pct      -6.6646
6             total_profit  530528.5100
7               total_loss -563851.2900
8               total_fees       0.0000
9             max_drawdown -113004.2700
10        max_drawdown_pct     -20.2704
11                win_rate      45.9215
12               loss_rate      54.0785
13          winning_trades     152.0000
14           losing_trades     179.0000
15                 avg_pnl     -89.3372
16          avg_return_pct      -0.0160
17          avg_trade_bars       1.0000
18              avg_profit    3490.3191
19          avg_profit_pct       0.6958
20  avg_winning_trade_bars       1.0000
21                avg_loss   -3150.0072
22            avg_loss_pct      -0.6241
23   avg_losing_trade_bars       1.0000
24             largest_win   31157.9400
25         largest_win_pct       5.9200
26        largest_win_bars       1.0000
27            largest_loss  -12682.6000
28        largest_loss_pct      -2.3100
29       largest_loss_bars       1.0000
30                max_wins       8.0000
31              max_losses       7.0000
32                  sharpe      -0.0132
33                 sortino      -0.0231
34           profit_factor       0.9638
35             ulcer_index       1.7639
36                     upi      -0.0039
37               equity_r2       0.5876
38               std_error   27448.1177
```