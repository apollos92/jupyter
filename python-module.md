
![shell](https://wikidocs.net/images/page/3139/05.07.png)

- 그림 5.7 파이썬 IDLE에서 새 파일 열기

새 창에 다음과 같이 코드를 작성합니다. 
앞에서 구현한 상한가와 하한가를 구하는 함수를 그대로 구현하고 추가로 author라는 변수가 pystock이라는 문자열을 바인딩하게 했습니다. 

``` python
def cal_upper(price):
    increment = price * 0.3
    upper_price = price + increment
    return upper_price

def cal_lower(price):
    decrement = price * 0.3
    lower_price = price - decrement
    return lower_price

author = 'pystock'
```

코드를 작성하고 나면 File 메뉴에서 Save 메뉴를 클릭해 파일로 저장합니다

![save](https://wikidocs.net/images/page/3139/05.08.png)

파이썬 코드를 파일로 저장할 때 저장될 파일의 경로를 `C:/Anaconda3` 디렉터리로 선택한 후 파일명을 stock으로 변경하고 저장 버튼을 클릭합니다. 
따라서 방금 작성한 코드의 저장 경로는 `C:/Anaconda3/stock.py`가 됩니다.

![](https://wikidocs.net/images/page/3139/05.09.png)


지금까지 작업한 내용을 요약해보면 함수를 구현하고 이를 `stock.py`라는 이름으로 하드디스크에 저장했습니다. 

이제 앞에서 작성한 stock이라는 모듈을 사용해 보겠습니다. 

파이썬 IDLE에서 stock 모듈을 임포트해 봅시다. 
여기서 오류가 발생하지 않으면 stock 모듈을 잘 만들었고 해당 모듈이 정상적으로 임포트된 것입니다.

![](https://wikidocs.net/images/page/3139/05.10.png)

앞에서 구현한 `stock` 모듈에는 `author`라는 변수와 `cal_upper`와 `cal_lower`라는 함수가 있었습니다. 

파이썬에서는 모듈을 임포트하면 모듈 내에 구현된 함수나 변수를 사용할 수 있습니다. 
- 모듈 내의 함수나 변수명에 접근할 때는 항상 `모듈명.함수명(변수명)`과 같은 형태로 적어야 합니다. 
- author라는 변수명을 바로 적으면 안 되고 stock.author라고 적어야 합니다. </p>

``` python
>>> print(stock.author)
pystock
>>>
```


stock 모듈 내에 구현된 함수를 호출해 보겠습니다. 
함수 역시 먼저 모듈명을 적은 후 '.'를 붙이고 함수명을 적어야 합니다. 

``` python
>>> stock.cal_upper(10000)
13000.0
>>> stock.cal_lower(10000)
7000.0
>>>
```
모듈 파일 내에서 함수를 직접 호출하는 테스트 코드를 구현하는 것이 좋습니다.
- `stock.py` 파일에 `cal_upper`와 `cal_lower` 함수를 호출하는 코드를 추가해 줍니다. 
- 그리고 `print(__name__)`도 추가해줍니다.

``` python
def cal_upper(price):
    increment = price * 0.3
    upper_price = price + increment
    return upper_price

def cal_lower(price):
    decrement = price * 0.3
    lower_price = price - decrement
    return lower_price

author = 'pystock'

print(cal_upper(10000))
print(cal_lower(10000))
print(__name__)
```

수정된 `stock.py` 파일을 실행하려면 `Run` - `Run Module` 메뉴를 차례로 선택합니다. 
![](https://wikidocs.net/images/page/3139/05.11.png)

파이썬 IDLE에 다음과 같이 stock.py 파일의 실행 결과가 출력됩니다. 

``` python
>>> 
======================= RESTART: C:\Anaconda3\stock.py =======================
13000.0
7000.0
__main__
>>>
```


업데이트된 stock 모듈을 다시 임포트 해보겠습니다. 

``` python
>>> import stock
13000.0
7000.0
stock
>>>
```

모듈을 직접 실행했을 때는 `print(__name__)`의 결과로 `__main__`이라는 문자열이 출력되지만, 해당 모듈을 임포트했을 때는 모듈의 이름인 `stock`이라는 문자열이 출력된다는 점입니다. 

파이썬에서 `__name__`이라는 변수는 파이썬 자체에서 사용하는 변수로, 특정 파이썬 파일이 직접 실행된 것인지 또는 다른 파이썬 파일에서 임포트 된 것인지를 확인하는 용도로 사용됩니다. 
- 특정 파이썬 파일이 독립적으로 실행됐다면 `__name__`이라는 변수는 `"__main__"`이라는 문자열을 바인딩하며 다른 파일에 임포트 된 경우에는 자신의 파일명을 바인딩합니다.

파이썬의 `__name__`이라는 변수를 사용하면 앞서 모듈의 테스트 코드가 모듈을 임포트했을 때 자동으로 호출되는 문제를 해결할 수 있습니다. 
stock.py 파일에 추가했던 테스트 코드를 다음과 같이 수정합니다.

``` python
if __name__ == "__main__":
    print(cal_upper(10000))
    print(cal_lower(10000))
    print(__name__)
```

- `__name__`이라는 파이썬 변수가 바인딩하고 있는 값이 `"__main__"`이라는 문자열이라면 들여쓰기 된 세 개의 `print`문을 실행합니다. 즉, `stock.py` 파일이 직접 실행이 된 경우라면 세 개의 `print`문이 실행됩니다. 
- 다른 파일에 `stock.py` 파일(모듈)이 임포트 된다면 `__name__`은 모듈의 이름인 `"stock"`을 바인딩하므로 if 문의 조건식을 만족하지 않고 따라서 세 개의 print문도 실행되지 않습니다.


`stock.py` 파일을 직접 실행시키면 다음과 같이 여전히 테스트가 코드가 출력됨을 확인할 수 있습니다.

``` python
>>> 
======================= RESTART: C:\Anaconda3\stock.py =======================
13000.0
7000.0
__main__
>>>
```