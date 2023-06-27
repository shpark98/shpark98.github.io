---
published: true

layout: single

title: "[Python] __main__, __init__.py"

categories: Python

tags: Python

toc: true

toc_label : 목차

toc_sticky: true

author_profile: false

sidebar :
    nav : "docs"
---

### if \_\_name\_\_ == \_\_main\_\_ 



#### 어떤 것을 의미하는가?

- 파이썬 스크립트 파일은 2가지 방법으로 실행될 수 있음.

1. 스크립트 파일이 직접 실행되는 경우

2. 다른 스크립트 파일에서 import 되어서 모듈로써 실행되는 경우 

   

`if __name__ == "__main__" ` 는 스크립트 파일이 직접 실행되는 경우에 실행되는 조건문

- 다른 스크립트 파일에서 import 되어 사용되는 경우에는 실행되지 않음



#### 왜 사용하는가?

```python
def calculate_square(n):
    return n * n

if __name__ == "__main__":
    num = 5
    result = calculate_square(num)
    print(f"The square of {num} is {result}.")
```

다음 파이썬 스크립트 같은 경우 직접 실행되면 `calculate_square` 함수를 사용하여 5의 제곱을 계산하고 결과를 출력함 

하지만 이 파이썬 스크립트 파일을 import 하여 다른 스크립트 파일에서 실행될 경우 아래의 조건문은 실행되지 않음

또한 calculate_square 함수를 사용하여 다른 작업에 활용할 수 있음



이와 같이 스크립트 파일을 모듈과 메인 프로그램으로 유연하게 사용할 수 있음



### \_\_init\_\_.py



#### 어떤 것을 의미하는가?

- 해당 디렉터리가 패키지의 일부임을 알려주는 역할을 함

- 패키지에 포함된 디렉터리에 `__init.py__` 파일이 없으면 패키지로 인식되지 않음 
  - python 3.3 버전부터는 해당 파일이 없어도 패키지로 인식하지만, 하위 버전 호환을 위해 파일	을 생성하는 것이 안전한 방법



