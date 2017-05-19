# Python / Jupyter Notebook 설치

## 개요

## Python 설치

### yum 활용

```
sudo yum install epel-release
```

```
sudo yum install python34

```


### 패키지 관리자 (pip) 설치

To install pip and setuptools, you need to install them separately as follows.

curl -O https://bootstrap.pypa.io/get-pip.py
sudo /usr/bin/python3.4 get-pip.py


## 연동 모듈 설치

### 의존 패키지 설치


``` bash
pip3 install pandas
```

```
Collecting pandas
  Downloading pandas-0.20.1-cp34-cp34m-manylinux1_x86_64.whl (24.3MB)
    100% |████████████████████████████████| 24.3MB 56kB/s
Collecting numpy>=1.7.0 (from pandas)
  Downloading numpy-1.12.1-cp34-cp34m-manylinux1_x86_64.whl (16.8MB)
    100% |████████████████████████████████| 16.8MB 81kB/s
Collecting python-dateutil>=2 (from pandas)
  Downloading python_dateutil-2.6.0-py2.py3-none-any.whl (194kB)
    100% |████████████████████████████████| 194kB 1.3MB/s
Collecting pytz>=2011k (from pandas)
  Downloading pytz-2017.2-py2.py3-none-any.whl (484kB)
    100% |████████████████████████████████| 491kB 956kB/s
Requirement already satisfied: six>=1.5 in /usr/lib/python3.4/site-packages (from python-dateutil>=2->pandas)
Installing collected packages: numpy, python-dateutil, pytz, pandas
Successfully installed numpy-1.12.1 pandas-0.20.1 python-dateutil-2.6.0 pytz-2017.2
```

## Jupyter Notebook 준비

### 설치

``` bash
pip3 install jupyter
```

```
...
Successfully built tornado pandocfilters terminado simplegeneric typing MarkupSafe
Installing collected packages: simplegeneric, decorator, typing, ptyprocess, pexpect, ipython-genutils, traitlets, jedi, pygments, wcwidth, prompt-toolkit, pickleshare, ipython, backports-abc, tornado, pyzmq, jupyter-core, jupyter-client, ipykernel, qtconsole, jsonschema, nbformat, pandocfilters, MarkupSafe, jinja2, webencodings, html5lib, bleach, entrypoints, mistune, testpath, nbconvert, jupyter-console, terminado, notebook, widgetsnbextension, ipywidgets, jupyter
Successfully installed MarkupSafe-1.0 backports-abc-0.5 bleach-2.0.0 decorator-4.0.11 entrypoints-0.2.2 html5lib-0.999999999 ipykernel-4.6.1 ipython-6.0.0 ipython-genutils-0.2.0 ipywidgets-6.0.0 jedi-0.10.2 jinja2-2.9.6 jsonschema-2.6.0 jupyter-1.0.0 jupyter-client-5.0.1 jupyter-console-5.1.0 jupyter-core-4.3.0 mistune-0.7.4 nbconvert-5.1.1 nbformat-4.3.0 notebook-5.0.0 pandocfilters-1.4.1 pexpect-4.2.1 pickleshare-0.7.4 prompt-toolkit-1.0.14 ptyprocess-0.5.1 pygments-2.2.0 pyzmq-16.0.2 qtconsole-4.3.0 simplegeneric-0.8.1 terminado-0.6 testpath-0.3 tornado-4.5.1 traitlets-4.3.2 typing-3.6.1 wcwidth-0.1.7 webencodings-0.5.1 widgetsnbextension-2.0.0

```


### 환경 설정

- 기본 환경 디렉터리: `~/.jupyter`

- 환경 디렉터리 변경: `JUPYTER_CONFIG_DIR` 환경 변수 등록

``` bash

```

- 노트북 문서 디렉터리 설정: `JUPYTER_PATH` 환경 변수에 OS별 디렉터리 구분자 활용, 추가

``` bash
```

### 설정파일 생성

- Notebook

```
jupyter notebook --generate-config
```

- `JUPYTER_CONFIG_DIR` 디렉터리 안에 `jupyter_notebook_config.py` 파일 생성

### 원격 접속 관련

#### password 설정

- Password 생성

``` python
from notebook.auth import passwd
passwd()
```

```
Enter password:
Verify password:
'sha1:...'
```

- `'sha1:...'` 영역을 복사, 생성한 설정파일 내 다음 항목 수정

> `jupyter_notebook_config.py` 파일 설정

``` python
...
c.NotebookApp.ip = '*'
c.NotebookApp.password = u'sha1:...'
c.NotebookApp.notebook_dir = u'/usr/local/share/jupyter'
```


## 실행

### 기본 명령

```
jupyter notebook
```

- 기본적으로 http://localhost:8888 에 대한 기본 브라우저 페이지 띄움 (띄울수 없으면 WARN 메시지)

### 실행 옵션

#### 기본 페이지 띄우지 않음

```
jupyter notebook --no-browser
```
