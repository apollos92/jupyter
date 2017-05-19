# Python / Jupyter Notebook 설치

## Python 준비

### Windows / MacOS

> 2017-05-19 현재 최신버전: `3.6.1`

- 공식 다운로드 페이지: https://www.python.org/downloads/release/python-361/

- 다운로드 후 패키지 설치 (관리자 권한 필요)


### 리눅스

> `root`, 또는 `sudo` 활용해 관리자 권한으로 설치

#### 바이너리 패키지 설치

> 리눅스 CentOS7 기준, `yum` 패키지 관리자 사용
> - 2017-05-19 현재 `EPEL` 등록 최신 버전: `3.4`

```
yum install epel-release
```

```
yum install python34
```

#### 참고: 최신 버전 설치 

> 소스 `tar` 이미지 다운, 직접 컴파일 필요

- 개발 패키지 설치

```
yum -y install zlib-devel
```

- 소스 다운 및 컴파일

> 2017-05-19 현재 최신버전: `3.6.1`

```
wget https://www.python.org/ftp/python/3.6.1/Python-3.6.1.tar.xz
tar xJf Python-3.6.0.tar.xz
cd Python-3.6.0
./configure
make
make install
```

## 모듈 관리자 (pip) 설치

- 아래와 같이 pip 설치용 파이썬 파일을 다운받아, `pip` 설치

> `pip` 활용, 나머지 필요 모듈 (`pandas`, `jupyter` 및 의존 모듈) 설치

```
curl -O https://bootstrap.pypa.io/get-pip.py
sudo /usr/bin/python3.4 get-pip.py
```

## 필요 모듈 설치

### Data Frame 모듈 설치 (`pandas`)

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

# Jupyter Notebook 준비

## 설치

``` bash
pip3 install jupyter
```

```
...
Successfully built tornado pandocfilters terminado simplegeneric typing MarkupSafe
Installing collected packages: simplegeneric, decorator, typing, ptyprocess, pexpect, ipython-genutils, traitlets, jedi, pygments, wcwidth, prompt-toolkit, pickleshare, ipython, backports-abc, tornado, pyzmq, jupyter-core, jupyter-client, ipykernel, qtconsole, jsonschema, nbformat, pandocfilters, MarkupSafe, jinja2, webencodings, html5lib, bleach, entrypoints, mistune, testpath, nbconvert, jupyter-console, terminado, notebook, widgetsnbextension, ipywidgets, jupyter
Successfully installed MarkupSafe-1.0 backports-abc-0.5 bleach-2.0.0 decorator-4.0.11 entrypoints-0.2.2 html5lib-0.999999999 ipykernel-4.6.1 ipython-6.0.0 ipython-genutils-0.2.0 ipywidgets-6.0.0 jedi-0.10.2 jinja2-2.9.6 jsonschema-2.6.0 jupyter-1.0.0 jupyter-client-5.0.1 jupyter-console-5.1.0 jupyter-core-4.3.0 mistune-0.7.4 nbconvert-5.1.1 nbformat-4.3.0 notebook-5.0.0 pandocfilters-1.4.1 pexpect-4.2.1 pickleshare-0.7.4 prompt-toolkit-1.0.14 ptyprocess-0.5.1 pygments-2.2.0 pyzmq-16.0.2 qtconsole-4.3.0 simplegeneric-0.8.1 terminado-0.6 testpath-0.3 tornado-4.5.1 traitlets-4.3.2 typing-3.6.1 wcwidth-0.1.7 webencodings-0.5.1 widgetsnbextension-2.0.0

```


## 환경 설정

### 환경 디렉터리 확인 (변경)

- 기본 환경 디렉터리: `~/.jupyter`

- 환경 디렉터리 변경: `.bash_profile` 등 계정 환경설정에 `JUPYTER_CONFIG_DIR` 환경 변수 등록

``` bash
...
JUPYTER_CONFIG_DIR = [환경변수 디렉터리]
...
export JUPYTER_CONFIG_DIR
```

### 설정파일 생성/수정


#### 생성 (`jupyter_notebook_config.py`)

- 환경 디렉터리 이동 후, 다음 명령 실행 

```
jupyter notebook --generate-config
```

- `jupyter_notebook_config.py` 파일 생성됨 확인

#### 설정파일 수정 

- `jupyter_notebook_config.py` 수정

- 예: 노트북 파일 (`.ipynb`) 홈 디렉터리 수정

``` python
...
c.NotebookApp.notebook_dir = '/usr/local/share/jupyter'
```

- 예: 임의 IP의 원격 접속 허용 (보안 이슈 있으므로, 신중히 선택)

``` python
...
c.NotebookApp.ip = '*'
```

#### password 설정 (원격 접속시 반드시 필요)

- Python REPL 에서 패스워드 생성 명령 실행

``` python
from notebook.auth import passwd
passwd()
```
- 패스워드 입력 후 암호화된 문자열 확인

```
Enter password:
Verify password:
'sha1:...'
```

- 암호화된 `'sha1:...'` 영역을 복사, 생성한 설정파일 내 다음 항목 수정

``` python
...
c.NotebookApp.password = 'sha1:...'
...
```

## 실행

### 기본 실행 명령

```
jupyter notebook
```

> http://localhost:8888 에 대한 기본 브라우저 페이지 띄움 (띄울수 없으면 WARN 메시지)

### 브라우저 띄우지 않고 실행

```
jupyter notebook --no-browser
```

### 백그라운드 실행 

```
nohup jupyter notebook --no-browser  1>/dev/null 2>/var/log/jupyter/jupyter.log &
```

### 페이지 접속

`http://[호스트 주소]:8888`

> 접속 후 미리 설정한 암호 입력하면, 노트북 목록 페이지로 이동함