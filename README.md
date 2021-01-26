# Introduction
In this project we were tasked with exploring the research question of how languages changed in the past and which factors contributed to that change. To this end we were considering to find data sets about the current number and historical data of speakers for a given language. Also we considered looking into obtaining data sets for related information, such as possibly census data. Then we would integrate those data sources in a meaningful way to be able to study language change.

However, we discarded this trajectory for two main reasons. First, data about the historical development of number of speakers for languages would require huge effort to create, especially for non-mainstream languages. Most likely any such data curation would be clouded by the the lack of good definition for the concept of _speaker_ as well. Does this term only encompass native speakers or should people speaking a language that they consciously acquired as well? If so, what is the language proficiency threshold to consider someone learning a second/third/... language as a proper speaker? Additionally one is faced with the problem of defining the term _language_ and its differentation from dialects as well. This is compounded by the fact that languages are often separated (or not separated) from dialects according to political motivations.

As a consequence of this we narrowed the scope for this project down to studying change for a specific spoken language roughly over the past one hundred years. We are mostly focusing on word frequencies, but there are more aspects one could look into such as semantic, syntactic or phonetic changes.


# Installation
This Project uses two fairly large datasets.
How to get the full datasets are described in section 2.2.1 and 3.1 in the jupyter notebook.

However, the full datasets are huge, and we are only using a small subset, which we've made available on https://drive.google.com/file/d/1Odg_vpAXTmonnaHMgYFe66orW_UqB_XZ/view?usp=sharing

After downloading, the folders `decades` and `processedData` which are under the folder `BookSolution` are to be extracted into the same folder as the jupyter notebook.
The folder named `CC_BY` is to be extracted into the parent directory of the notebook.

# Hypothesis / Goal
Given a corpus of text documents that are associated with a certain publication year, which ideally comes equally distributed over the past 100 years, we looked into whether or not we can extract enough information to classify unseen text documents as belonging to a certain decade. As part of the implementation for this project we were looking into various methods for meeting this goal, which shall be explained in the coming sections.

# System description
For reproducability, We've attached a full description of the system where this was run:

## Operating System
```
$ lsb_release -a
No LSB modules are available.
Distributor ID:	Ubuntu
Description:	Ubuntu 20.04.1 LTS
Release:	20.04
Codename:	focal

```

## Python
```
$ python --version
Python 3.8.3

```


## Package Versions
```
$ pip freeze
aiohttp==3.7.3
aiohttp-cors==0.7.0
aioredis==1.3.1
alabaster==0.7.12
anaconda-client==1.7.2
anaconda-navigator==1.10.0
anaconda-project @ file:///tmp/build/80754af9/anaconda-project_1610472525955/work
anyio==2.0.2
appdirs==1.4.4
argh==0.26.2
argon2-cffi @ file:///tmp/build/80754af9/argon2-cffi_1596828493937/work
asn1crypto @ file:///tmp/build/80754af9/asn1crypto_1596577642040/work
astroid @ file:///tmp/build/80754af9/astroid_1592495912941/work
astropy @ file:///tmp/build/80754af9/astropy_1606922912494/work
async-generator==1.10
async-timeout==3.0.1
atomicwrites==1.4.0
attrs @ file:///tmp/build/80754af9/attrs_1604765588209/work
autopep8 @ file:///tmp/build/80754af9/autopep8_1596578164842/work
Babel @ file:///tmp/build/80754af9/babel_1607110387436/work
backcall==0.2.0
backports.functools-lru-cache @ file:///tmp/build/80754af9/backports.functools_lru_cache_1605305165209/work
backports.shutil-get-terminal-size @ file:///tmp/build/80754af9/backports.shutil_get_terminal_size_1608222128777/work
backports.tempfile @ file:///home/linux1/recipes/ci/backports.tempfile_1610991236607/work
backports.weakref==1.0.post1
beautifulsoup4 @ file:///home/linux1/recipes/ci/beautifulsoup4_1610988766420/work
bitarray @ file:///tmp/build/80754af9/bitarray_1611254360450/work
bkcharts==0.2
black==20.8b1
bleach @ file:///tmp/build/80754af9/bleach_1611254400839/work
blessings==1.7
bokeh @ file:///tmp/build/80754af9/bokeh_1603297833684/work
boto==2.49.0
Bottleneck==1.3.2
brotlipy==0.7.0
cachetools==4.2.0
certifi==2020.12.5
cffi @ file:///tmp/build/80754af9/cffi_1606255081583/work
chardet @ file:///tmp/build/80754af9/chardet_1607706746162/work
click @ file:///home/linux1/recipes/ci/click_1610990599742/work
cloudpickle @ file:///tmp/build/80754af9/cloudpickle_1598884132938/work
clyent==1.2.2
colorama @ file:///tmp/build/80754af9/colorama_1607707115595/work
colorful==0.5.4
conda==4.9.2
conda-build==3.18.11
conda-package-handling @ file:///tmp/build/80754af9/conda-package-handling_1603018141399/work
conda-verify==3.4.2
contextlib2==0.6.0.post1
cryptography @ file:///tmp/build/80754af9/cryptography_1607635341180/work
cycler==0.10.0
Cython @ file:///tmp/build/80754af9/cython_1605457646007/work
cytoolz==0.11.0
dask @ file:///tmp/build/80754af9/dask-core_1607706933335/work
decorator==4.4.2
defusedxml==0.6.0
diff-match-patch @ file:///tmp/build/80754af9/diff-match-patch_1594828741838/work
dill==0.3.3
distlib==0.3.1
distributed @ file:///tmp/build/80754af9/distributed_1610822560169/work
docutils==0.16
editdistance==0.5.3
entrypoints==0.3
et-xmlfile==1.0.1
fastcache==1.1.0
filelock @ file:///home/linux1/recipes/ci/filelock_1610993975404/work
flake8 @ file:///tmp/build/80754af9/flake8_1601911421857/work
Flask==1.1.2
fsspec==0.8.5
future==0.18.2
gensim==3.8.3
gevent @ file:///tmp/build/80754af9/gevent_1610995009582/work
glob2 @ file:///home/linux1/recipes/ci/glob2_1610991677669/work
gmpy2==2.0.8
google==3.0.0
google-api-core==1.25.0
google-auth==1.24.0
googleapis-common-protos==1.52.0
gpustat==0.6.0
greenlet==1.0.0
grpcio==1.34.1
h5py==3.1.0
HeapDict==1.0.1
helpdev==0.7.1
hiredis==1.1.0
html5lib @ file:///tmp/build/80754af9/html5lib_1593446221756/work
idna==3.1
imagecodecs @ file:///tmp/build/80754af9/imagecodecs_1611258060730/work
imageio @ file:///tmp/build/80754af9/imageio_1594161405741/work
imagesize==1.2.0
importlib-metadata==3.4.0
iniconfig @ file:///home/linux1/recipes/ci/iniconfig_1610983019677/work
intervaltree @ file:///tmp/build/80754af9/intervaltree_1598376443606/work
ipykernel==5.4.3
ipython @ file:///tmp/build/80754af9/ipython_1610724799192/work
ipython-genutils @ file:///tmp/build/80754af9/ipython_genutils_1606773439826/work
ipywidgets @ file:///tmp/build/80754af9/ipywidgets_1610481889018/work
isort==5.7.0
itsdangerous==1.1.0
jdcal==1.4.1
jedi==0.18.0
jeepney @ file:///tmp/build/80754af9/jeepney_1606148855031/work
Jinja2 @ file:///home/linux1/recipes/ci/jinja2_1610990516718/work
joblib @ file:///tmp/build/80754af9/joblib_1607970656719/work
json5==0.9.5
jsonschema @ file:///tmp/build/80754af9/jsonschema_1602607155483/work
jupyter==1.0.0
jupyter-client==6.1.11
jupyter-console @ file:///tmp/build/80754af9/jupyter_console_1598884538475/work
jupyter-contrib-core==0.3.3
jupyter-contrib-nbextensions @ file:///home/conda/feedstock_root/build_artifacts/jupyter_contrib_nbextensions_1602805456242/work
jupyter-core @ file:///tmp/build/80754af9/jupyter_core_1606148996965/work
jupyter-highlight-selected-word @ file:///home/conda/feedstock_root/build_artifacts/jupyter_highlight_selected_word_1611341001732/work
jupyter-latex-envs @ file:///home/conda/feedstock_root/build_artifacts/jupyter_latex_envs_1602788792978/work
jupyter-nbextensions-configurator @ file:///home/conda/feedstock_root/build_artifacts/jupyter_nbextensions_configurator_1611341108640/work
jupyter-server==1.2.2
jupyterlab==3.0.5
jupyterlab-pygments @ file:///tmp/build/80754af9/jupyterlab_pygments_1601490720602/work
jupyterlab-server==2.1.2
jupyterlab-widgets @ file:///tmp/build/80754af9/jupyterlab_widgets_1609884341231/work
keyring @ file:///tmp/build/80754af9/keyring_1609353669393/work
kiwisolver==1.3.1
lazy-object-proxy==1.5.2
libarchive-c @ file:///home/linux1/recipes/ci/python-libarchive-c_1610974153025/work
llvmlite==0.34.0
locket==0.2.1
lxml @ file:///tmp/build/80754af9/lxml_1606516814318/work
MarkupSafe==1.1.1
matplotlib==3.3.3
mccabe==0.6.1
mistune==0.8.4
mkl-fft==1.2.0
mkl-random==1.1.1
mkl-service==2.3.0
mock @ file:///tmp/build/80754af9/mock_1607622725907/work
more-itertools @ file:///tmp/build/80754af9/more-itertools_1605111547926/work
mpmath==1.1.0
msgpack==1.0.2
multidict==5.1.0
multipledispatch==0.6.0
multiprocess==0.70.11.1
mypy-extensions==0.4.3
navigator-updater==0.2.1
nb-conda==2.2.1
nb-conda-kernels @ file:///tmp/build/80754af9/nb_conda_kernels_1606775941989/work
nbclassic==0.2.6
nbclient @ file:///tmp/build/80754af9/nbclient_1602783176460/work
nbconvert @ file:///tmp/build/80754af9/nbconvert_1601914830498/work
nbformat @ file:///tmp/build/80754af9/nbformat_1610738111109/work
nest-asyncio @ file:///tmp/build/80754af9/nest-asyncio_1606153767164/work
networkx @ file:///tmp/build/80754af9/networkx_1598376031484/work
nltk @ file:///tmp/build/80754af9/nltk_1592496090529/work
nose @ file:///tmp/build/80754af9/nose_1606773131901/work
notebook @ file:///tmp/build/80754af9/notebook_1611340975709/work
numba @ file:///tmp/build/80754af9/numba_1600100669015/work
numexpr @ file:///tmp/build/80754af9/numexpr_1609354661181/work
numpy==1.19.5
numpydoc @ file:///tmp/build/80754af9/numpydoc_1605117425582/work
nvidia-ml-py3==7.352.0
olefile==0.46
opencensus==0.7.12
opencensus-context==0.1.2
openpyxl @ file:///tmp/build/80754af9/openpyxl_1610651698508/work
packaging @ file:///tmp/build/80754af9/packaging_1607971725249/work
pandas==1.2.1
pandocfilters @ file:///tmp/build/80754af9/pandocfilters_1605120460739/work
parso==0.8.1
partd==1.1.0
path @ file:///tmp/build/80754af9/path_1607537225611/work
pathlib2 @ file:///tmp/build/80754af9/pathlib2_1607024983162/work
pathos==0.2.7
pathspec==0.8.1
pathtools==0.1.2
patsy==0.5.1
pep8==1.7.1
pexpect @ file:///tmp/build/80754af9/pexpect_1605563209008/work
pickleshare @ file:///tmp/build/80754af9/pickleshare_1606932040724/work
Pillow @ file:///tmp/build/80754af9/pillow_1609786786540/work
pkginfo==1.7.0
pluggy==0.13.1
ply==3.11
POT==0.7.0
pox==0.2.9
ppft==1.6.6.3
prometheus-client @ file:///tmp/build/80754af9/prometheus_client_1606344362066/work
prompt-toolkit==3.0.10
protobuf==3.14.0
psutil==5.8.0
ptyprocess @ file:///tmp/build/80754af9/ptyprocess_1609355006118/work/dist/ptyprocess-0.7.0-py2.py3-none-any.whl
py @ file:///tmp/build/80754af9/py_1607971587848/work
py-spy==0.3.3
pyasn1==0.4.8
pyasn1-modules==0.2.8
pycodestyle==2.6.0
pycosat==0.6.3
pycparser @ file:///tmp/build/80754af9/pycparser_1594388511720/work
pycurl==7.43.0.6
pydocstyle @ file:///tmp/build/80754af9/pydocstyle_1598885001695/work
pyerfa @ file:///tmp/build/80754af9/pyerfa_1606860180519/work
pyflakes==2.2.0
Pygments @ file:///tmp/build/80754af9/pygments_1610565767015/work
pylint @ file:///tmp/build/80754af9/pylint_1598623985952/work
pyls-black @ file:///tmp/build/80754af9/pyls-black_1607553132291/work
pyls-spyder @ file:///tmp/build/80754af9/pyls-spyder_1608134179673/work
pyodbc==4.0.30
pyOpenSSL @ file:///tmp/build/80754af9/pyopenssl_1608057966937/work
pyparsing @ file:///home/linux1/recipes/ci/pyparsing_1610983426697/work
PyQt5==5.15.2
PyQt5-sip==12.8.1
PyQtWebEngine==5.15.2
pyrsistent @ file:///tmp/build/80754af9/pyrsistent_1600141720057/work
PySocks @ file:///tmp/build/80754af9/pysocks_1605305779399/work
pytest==6.2.1
python-dateutil==2.8.1
python-jsonrpc-server @ file:///tmp/build/80754af9/python-jsonrpc-server_1600278539111/work
python-language-server @ file:///tmp/build/80754af9/python-language-server_1607972495879/work
pytz @ file:///tmp/build/80754af9/pytz_1608922264688/work
PyWavelets @ file:///tmp/build/80754af9/pywavelets_1601658317819/work
pyxdg @ file:///tmp/build/80754af9/pyxdg_1603822279816/work
PyYAML==5.4.1
pyzmq==21.0.1
QDarkStyle==2.8.1
QtAwesome==1.0.2
qtconsole==5.0.1
QtPy==1.9.0
ray==1.1.0
redis==3.5.3
regex @ file:///tmp/build/80754af9/regex_1606772724491/work
requests @ file:///tmp/build/80754af9/requests_1608241421344/work
rope @ file:///tmp/build/80754af9/rope_1602264064449/work
rsa==4.7
Rtree==0.9.7
ruamel-yaml==0.15.87
ruamel.yaml.clib==0.2.2
scikit-image==0.18.1
scikit-learn==0.24.0
scipy==1.6.0
seaborn @ file:///tmp/build/80754af9/seaborn_1608578541026/work
SecretStorage @ file:///tmp/build/80754af9/secretstorage_1606864733683/work
Send2Trash @ file:///tmp/build/80754af9/send2trash_1607525499227/work
simplegeneric==0.8.1
singledispatch @ file:///tmp/build/80754af9/singledispatch_1602523705405/work
sip==6.0.0
six @ file:///tmp/build/80754af9/six_1605205327372/work
sklearn==0.0
smart-open==4.1.0
sniffio==1.2.0
snowballstemmer @ file:///tmp/build/80754af9/snowballstemmer_1611258885636/work
sortedcollections @ file:///tmp/build/80754af9/sortedcollections_1611172717284/work
sortedcontainers @ file:///tmp/build/80754af9/sortedcontainers_1606865132123/work
soupsieve @ file:///tmp/build/80754af9/soupsieve_1607965878077/work
Sphinx @ file:///tmp/build/80754af9/sphinx_1610133430332/work
sphinxcontrib-applehelp==1.0.2
sphinxcontrib-devhelp==1.0.2
sphinxcontrib-htmlhelp==1.0.3
sphinxcontrib-jsmath==1.0.1
sphinxcontrib-qthelp==1.0.3
sphinxcontrib-serializinghtml==1.1.4
sphinxcontrib-websupport @ file:///tmp/build/80754af9/sphinxcontrib-websupport_1597081412696/work
spyder==4.2.1
spyder-kernels @ file:///tmp/build/80754af9/spyder-kernels_1608578795921/work
SQLAlchemy==1.3.22
statsmodels @ file:///tmp/build/80754af9/statsmodels_1606865674184/work
sympy @ file:///tmp/build/80754af9/sympy_1608137652302/work
tables==3.6.1
tblib @ file:///tmp/build/80754af9/tblib_1597928476713/work
terminado==0.9.2
testpath==0.4.4
textdistance==4.2.0
threadpoolctl @ file:///tmp/tmp9twdgx9k/threadpoolctl-2.1.0-py3-none-any.whl
three-merge @ file:///tmp/build/80754af9/three-merge_1607553261110/work
tifffile @ file:///tmp/build/80754af9/tifffile_1610739638720/work
toml==0.10.2
toolz @ file:///home/linux1/recipes/ci/toolz_1610987900194/work
tornado @ file:///tmp/build/80754af9/tornado_1606942300299/work
tqdm==4.56.0
traitlets @ file:///tmp/build/80754af9/traitlets_1602787416690/work
typed-ast @ file:///tmp/build/80754af9/typed-ast_1610484547928/work
typing-extensions @ file:///tmp/build/80754af9/typing_extensions_1598376058250/work
ujson @ file:///tmp/build/80754af9/ujson_1611259522456/work
unicodecsv==0.14.1
urllib3 @ file:///tmp/build/80754af9/urllib3_1606938623459/work
virtualenv==20.3.1
watchdog==1.0.2
wcwidth @ file:///tmp/build/80754af9/wcwidth_1593447189090/work
webencodings==0.5.1
Werkzeug==1.0.1
widgetsnbextension==3.5.1
wrapt==1.12.1
wurlitzer @ file:///tmp/build/80754af9/wurlitzer_1594753850195/work
xlrd @ file:///tmp/build/80754af9/xlrd_1608072521494/work
XlsxWriter @ file:///tmp/build/80754af9/xlsxwriter_1602692860603/work
xlwt==1.3.0
xmltodict==0.12.0
yapf @ file:///tmp/build/80754af9/yapf_1593528177422/work
yarl==1.6.3
zict==2.0.0
zipp @ file:///tmp/build/80754af9/zipp_1604001098328/work
zope.event==4.5.0
zope.interface @ file:///tmp/build/80754af9/zope.interface_1606940259012/work
```

## System
```
$ sudo lshw -short
[sudo] password for <user>: 
H/W path           Device     Class          Description
========================================================
                              system         20QN0034MX (LENOVO_MT_20QN_BU_Think_FM_ThinkPad P53)
/0/3                          memory         128GiB System Memory
/0/f                          memory         384KiB L1 cache
/0/10                         memory         1536KiB L2 cache
/0/11                         memory         12MiB L3 cache
/0/12                         processor      Intel(R) Core(TM) i7-9850H CPU @ 2.60GHz
/0/13                         memory         128KiB BIOS
/0/100                        bridge         8th Gen Core Processor Host Bridge/DRAM Registers
/0/100/1                      bridge         Xeon E3-1200 v5/E3-1500 v5/6th Gen Core Processor PCIe Controller (x16)
/0/100/1/0                    display        TU106GLM [Quadro RTX 3000 Mobile / Max-Q]
...
/0/100/2           /dev/fb0   display        UHD Graphics 630 (Mobile)
/0/100/4                      generic        Xeon E3-1200 v5/E3-1500 v5/6th Gen Core Processor Thermal Subsystem
/0/100/8                      generic        Xeon E3-1200 v5/v6 / E3-1500 v5 / 6th/7th/8th Gen Core Processor Gaussian Mixture Model
```