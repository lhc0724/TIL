# Python Module and Package
파이썬의 모듈과 패키지의 차이를 구분하고 사용법을 정리하였습니다.

> PSL(Python Standard Library): 파이썬에 기본으로 내장된 모듈과 패키지의 묶음.  
> 간단히 집고 가는 것으로 해당 문서에는 파이썬 표준 라이브러리에 대해 서술 하지 않음.
  
## 1. Module
특정 기능(global variable, function, etc...)들을 .py 파일 단위로 작성한 것.

예)  shapes.py
```python
    def triangle():
        print("삼각형")
    
    def square():
        print("사각형")
```

### Use Module
``` python
    import shapes

    shapes.triangle()
    # '삼각형' 출력

    shapes.square()
    # '사각형' 출력
```

## 2. Package
패키지는 모듈들을 디렉토리 형식으로 구조화한 형태.  
도트(.)를 사용하여 계층적으로 쉽게 관리 할 수 있다.  
  
### 2-1. 패키지의 구조
패키지의 이름은 모듈들이 있는 디렉토리의 이름이 된다. ( package name = directory name )  
  
패키지 디렉토리는 \_\_init\_\_.py 를 포함하는데, 이는 해당 디렉토리가 일반 폴더가 아닌 패키지 디렉토리임을 알린다. (\_\_init__.py의 내용은 빈 파일이어도 상관 없음.)   

> __Python 3.3__ 이후 버전 부터는 \_\_init\__.py 를 포함하지 않아도 패키지로 인식함.  
> 하지만 하위 버전의 __호환과 패키지 사용을 쉽게__ 하기에 작성하는 것을 권장.  


예) calculation package
``` 
calc/
    __init__.py

    operation/
        __init__.py
        add.py
        sub.py
        mult.py
        div.py

    calculus/    
        __init_.py
        differential.py
        integral.py
    
    area_calc/
        __init__.py
        triangle.py
        square.py
```

__calc__ 패키지 안에는 __operation, calculus, area_calc__ 세개의 하위 패키지가 포함된다.  

### 2-2. 패키지 사용하기  
> calc 패키지의 모듈들이 전부 구현 되어있다고 가정하여 작성.

사용 방법:
* import
* from * import
* direct function import  

```python
    # import package module
    # add 모듈은 calc/operation/add.py 파일
    import calc.operation.add
    
    calc.operation.add.func_add(5, 11)
    # 16출력.

    # from * import
    # clac/operation 디렉토리까지 접근 후 div모듈 import
    from calc.operation import div

    div.func_div(10/2)
    # 5출력. 모듈 명만 이용하여 함수 호출이 가능

    # direct function import
    # calc/area_calc/square.py 까지 접근 후 calc_area 라는 이름의 함수만을 import
    from calc.area_calc.triangle import calc_area

    calc_area(weight=10, height = 5)
    # 25출력. 함수를 바로 호출하여 사용.
```  

from * import 정리
> * from [패키지].[모듈] import 변수
> * from [패키지].[모듈] import 함수
> * from [패키지].[모듈] import 클래스

## 3. \_\_init__.py
위에서 설명했듯 \_\_init__.py는 내용이 없는 빈파일, 혹은 3.3버전 부턴 없어도 된다.  
하지만 큰 프로젝트에서 생산성을 증가 시켜주는 등 편의성에 큰 역할을 한다.

### 3-1. \_\_all__변수
@ calc/operation/\_\_init__.py
```python
    # __init__.py
    __all__ = ['add', 'sub']
```
```python
    from calc.operation import *

    add.func_add(5, 5) # 10 출력
    div.func_div(10, 2) # NameError: name 'func_div' is not defined
```

이처럼 패키지 경로에서 모듈을 전부 불렀을 때, 불러오는 모듈을 관리 할 수 있다.  

### 3-2. 자주 사용하는 모듈 간소화
@ calc/operation/add.py
```python
    import example
```
@ calc/operation/sub.py
```python
    import example
```

위처럼 패키지 내의 모듈들이 전부 같은 모듈을 import 할때, 각각 선언 해 주어야 하지만,  
해당 경로의 \_\_init__.py에 한번만 명시 하는 것으로 코드를 줄 일 수 있다.

@ calc/operation/\_\_init__.py
```python
    # __init__.py
    import example
```
해당 경로의 모든 .py 파일은 콩통으로 example을 사용 할 수 있게 된다.

### 3-3. 호출 간소화
<!-- > 설명하기 앞서 파이썬은 absolute path(절대경로)와 relative path(상대경로)를 지원한다.  
> 이들의 차이점은 __경로의 시작점이다__.  
> 절대경로는 프로젝트 최상단 디렉토리를 기준으로 import path를 찾는 반면  
> 상대경로는 현재 파일의 위치를 기준으로 삼는다. -->

@ calc/operation/\_\_init__.py
```python
    # __init__.py
    from .add import func_add
    from .sub import func_sub
    from .mult import func_multiplication
    from .div import func_div
```
relative import를 이용하여 현재 경로의 모듈내의 함수들을 모두 import 하였다.  
이를 통해 얼마나 코드가 간소화 되는지 확인해보자.
```python
    #main.py
    from calc import operation

    operation.func_add(10, 10) # 20출력
    operation.func_sub(20, 10) # 10출력
    ...
```
2-2에서 다룬 패키지 사용법보다 훨씬 간결해 진것을 확인 할 수 있다.