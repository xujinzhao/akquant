# 使用数据源

## 开源财经数据接口库

1. [AKShare](https://akshare.akfamily.xyz)
2. [YFinance](https://github.com/ranaroussi/yfinance/)
3. [Tushare](https://tushare.pro/)

## 国内财经数据源

国内的财经数据源包括但不限于：

1. [东方财富](https://www.eastmoney.com/)
2. [同花顺](https://www.10jqka.com.cn/)
3. [新浪财经](https://finance.sina.com.cn/)
4. [腾讯财经](https://finance.qq.com/)
5. [雪球](https://xueqiu.com/)
6. [金融界](https://www.jrj.com.cn/)
7. [聚宽](https://www.joinquant.com/)
8. [米筐](https://www.ricequant.com/)
9. [天勤](https://www.shinnytech.com/tensentq)
10. [优矿](https://uqer.io/home/)
11. [掘金](https://www.myquant.cn/)
12. [万矿](https://www.wmcloud.com/)
13. [通联数据](https://www.allinfinance.com/)
14. [恒有数](https://udata.hs.net/)

国内商业及学术研究数据源：

1. [CSMAR](https://data.csmar.com/)
2. [Wind](https://www.wind.com.cn/)
3. [CNRDS](https://www.cnrds.com/)

## 自定义数据源

PyBroker 提供了自定义数据源的功能，可以通过如下方式自定义数据源：

```python
import pandas as pd
import pybroker
from pybroker.data import DataSource

class CSVDataSource(DataSource):

    def __init__(self):
        super().__init__()
        # Register custom columns in the CSV.
        pybroker.register_columns('rsi')

    def _fetch_data(self, symbols, start_date, end_date, _timeframe, _adjust):
        df = pd.read_csv('data/prices.csv')
        df = df[df['symbol'].isin(symbols)]
        df['date'] = pd.to_datetime(df['date'])
        return df[(df['date'] >= start_date) & (df['date'] <= end_date)]
```