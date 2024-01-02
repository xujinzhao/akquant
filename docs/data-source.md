# 使用数据源

## 自定义数据源

PyBroker 提供了自定义数据源的功能，可以通过如下方式自定义数据源：

``` py title="ds_01.py" linenums="1" hl_lines="5 12"
import pandas as pd
import pybroker as pb
# 从 pybroker.data 模块中导入 DataSource 类，这个类是一个抽象基类
from pybroker.data import DataSource

# 定义一个名为 CSVDataSource 的类，该类继承自 DataSource
# 这个类代表了一个从 CSV 文件中检索数据的数据源
class CSVDataSource(DataSource):

    # CSVDataSource 类的构造方法
    def __init__(self):
        # 调用父类 DataSource 的构造方法，以正确初始化继承的属性或方法
        super().__init__()
        # 在 pybroker 系统中注册一个自定义的列标识符 'rsi'
        # 这表明 'rsi'（相对强弱指数）是 CSV 数据中的一个列名，需要被 pybroker 识别
        pybroker.register_columns('rsi')

    # 定义一个受保护的方法来从 CSV 文件中获取数据
    # 这个方法接受符号、开始日期、结束日期、_timeframe 和 _adjust 作为参数
    def _fetch_data(self, symbols, start_date, end_date, _timeframe, _adjust):
        # 将 CSV 数据读入一个 pandas DataFrame。pandas 特别适合处理 CSV 数据
        df = pd.read_csv('data/prices.csv')
        # 过滤 DataFrame，只包含 'symbol' 列与参数中提供的符号匹配的行
        df = df[df['symbol'].isin(symbols)]
        # 将 DataFrame 中的 'date' 列转换为 pandas 的 datetime 对象，以便更好地处理日期
        df['date'] = pd.to_datetime(df['date'])
        # 返回一个 DataFrame，其中包含指定开始和结束日期之间的行
        return df[(df['date'] >= start_date) & (df['date'] <= end_date)]
```
