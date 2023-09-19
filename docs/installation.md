# PyBroker 安装

PyBroker 目前支持在 Windows，macOS 和 Linux 中 Python 3.9 及以上版本，
建议使用 Python 3.11 及以上版本中进行安装和使用。

> 此处 Windows 用户需要注意，Windows 10 及以上版本才支持 Python 3.9 及以上版本。

> 由于 PyBroker 需要安装的依赖库比较多，
> 因此安装过程可能会比较慢，
> 建议使用 **[清华镜像源](https://mirrors.tuna.tsinghua.edu.cn/help/pypi/)** 进行安装。

## PIP 安装

### PyPI 镜像源安装

``` shell
pip install lib-pybroker -i https://pypi.org/simple
```

### 清华镜像源安装

``` shell
pip install lib-pybroker -i https://pypi.tuna.tsinghua.edu.cn/simple
```

## PIP 升级

### PyPI 镜像源升级

``` shell
pip install -U lib-pybroker -i https://pypi.org/simple
```

### 清华镜像源升级

``` shell
pip install -U lib-pybroker -i https://pypi.tuna.tsinghua.edu.cn/simple
```

## 源码安装

目前 PyBroker 项目的源码托管在 GitHub 平台，可以通过以下命令下载源码并安装：

``` shell
git clone https://github.com/edtechre/pybroker
cd pybroker
python setup.py install
```

> 此处不建议使用源码安装，源码中的对 PyBroker 需要的依赖库版本限制不够严格，比如使用 pandas 2.1.0
版本则目前不兼容。

## 查看版本

当成功安装 PyBroker 后，可以通过如下命令查看安装的版本：

```python
import pybroker as pb

print(pb.__version__)
```

结果显示：

```shell
1.1.29
```

## 依赖库

PyBroker 目前的依赖库比较多，
可以通过官网的 [requirements.txt](https://github.com/edtechre/pybroker/blob/master/requirements.txt)
查看最新的依赖：

```shell
akshare>=1.10.1
alpaca-py>=0.7.2
black>=22.10.0
diskcache>=5.4.0
flake8>=5.0.4
flake8-bugbear>=22.10.25
joblib>=1.2.0
jupyter>=1.0.0
matplotlib>=3.6.3
mypy>=0.982
nbsphinx>=0.8.11
numba>=0.56.3
numpy>=1.23.4
pandas>=1.5.1
progressbar2>=4.1.1
pytest>=7.2.0
pytest-cov>=4.0.0
pytest-instafail>=0.4.2
pytest-lazy-fixture>=0.6.3
pytest-randomly>=3.12.0
pytest-xdist>=3.0.2
scikit-learn>=1.2.1
Sphinx>=5.3.0
sphinx_rtd_theme>=1.1.1
sphinx-intl>=2.1.0
yfinance>=0.1.84
```

当然，也可以在本地环境中通过如下命令查看已安装的依赖库：

```shell
pip list
```

结果显示：

```shell
Package                    Version
-------------------------- ---------
akshare                    1.10.95
alpaca-py                  0.8.2
appdirs                    1.4.4
Babel                      2.12.1
beautifulsoup4             4.12.2
certifi                    2023.7.22
charset-normalizer         3.2.0
click                      8.1.7
colorama                   0.4.6
cssselect                  1.2.0
decorator                  5.1.1
diskcache                  5.6.3
et-xmlfile                 1.1.0
frozendict                 2.3.8
ghp-import                 2.1.0
html5lib                   1.1
idna                       3.4
Jinja2                     3.1.2
joblib                     1.3.2
jsonpath                   0.82.2
lib-pybroker               1.1.29
llvmlite                   0.40.1
lxml                       4.9.3
Markdown                   3.4.4
markdown2                  2.4.10
MarkupSafe                 2.1.3
mergedeep                  1.3.4
mkdocs                     1.5.2
mkdocs-material            9.2.6
mkdocs-material-extensions 1.1.1
msgpack                    1.0.5
multitasking               0.0.11
numba                      0.57.1
numpy                      1.24.4
openpyxl                   3.1.2
packaging                  23.1
paginate                   0.5.6
pandas                     1.5.3
pathspec                   0.11.2
pip                        23.2.1
platformdirs               3.10.0
progressbar2               4.2.0
py-mini-racer              0.6.0
pydantic                   1.10.12
Pygments                   2.16.1
pymdown-extensions         10.2.1
pypinyin                   0.49.0
pyquery                    2.0.0
python-dateutil            2.8.2
python-utils               3.7.0
pytz                       2023.3
PyYAML                     6.0.1
pyyaml_env_tag             0.1
readtime                   3.0.0
regex                      2023.8.8
requests                   2.31.0
setuptools                 68.0.0
tabulate                   0.9.0
tqdm                       4.66.1
typing_extensions          4.7.1
urllib3                    2.0.4
watchdog                   3.0.0
webencodings               0.5.1
websockets                 10.4
wheel                      0.38.4
xlrd                       2.0.1
yfinance                   0.2.28
```