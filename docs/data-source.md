# 使用数据源

## 自定义数据源

PyBroker 提供了自定义数据源的功能，可以通过如下方式自定义数据源：

``` py title="ds_01.py" linenums="1" hl_lines="5 12"
import pandas as pd
import pybroker as pb
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
