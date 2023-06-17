---
published: true

layout: single

title: "[Python] 파이썬 인자 값 추가, Argparse 모듈"

categories: Python

tags: Python

toc: true

toc_label : 목차

toc_sticky: true

author_profile: false

sidebar :
    nav : "docs"
---

## Argparse



### Argpasre 모듈이란?

파이썬 스크립트가 있고, 그 파이썬 파일을 명령 프롬프트에서 다음 명령어를 통해 실행할 수 있음

```bash
$ ./run.py
```



하지만 만약 어떤 옵션에 따라 파이썬 스크립트를 다르게 동작하게 해주려면 명령행을 통해 아래와 같이 인자를 받아야 함

run.py 스크립트에서 사용자가 입력한 명령 행의 인자를 파싱한 후 인자 값에 따라 적당한 동작을 수행해줘여 함

이렇게 명령 행의 인자를 파싱할 때 사용하는 모듈이 **Argparse **임



### Argparse

- 명령 행을 파싱하기 위해 argparse 모듈 import

```
# run.py
import argparse

# ArgumentParser로 parser 객체 생성
parser = argparse.ArgumentParser(description = "Argument 설명") # description 키워드를 이용하여 Argument 설명이나 프로그램 설명

# add_argument로 parser에 인자 추가
parser.add_argument("-d", "--decimal", dest="decimal", action="store")          # extra value
parser.add_argument("-f", "--fast", dest="fast", action="store_true")           # existence/nonexistence

# parse_args()를 통해 parser 객체의 인자들 파싱
args = parser.parse_args()

print(args.decimal)
print(args.fast)
```



#### ArgumentParser 객체

- ArgumentParser로 parser 객체 생성



##### 매개변수

- **prog**:  프로그램의 이름 (기본값: `sys.argv[0]`)
- **usage**: 프로그램 사용법을 설명하는 문자열 (기본값: 파서에 추가된 인자로부터 만들어지는 값)
- **description**:  인자 도움말 전에 표시할 텍스트 (기본값: `None`)
- **epilog:** 인자 도움말 후에 표시할 텍스트 (기본값: `None`)
- **parents:** `ArgumentParser` 객체들의 리스트이고, 이 들의 인자들도 포함
- **formatter_class:** 도움말 출력을 사용자 정의하기 위한 클래스
- **prefix_chars:** 선택 인자 앞에 붙는 문자 집합 (기본값: '-').
- **fromfile_prefix_chars:** 추가 인자를 읽어야 하는 파일 앞에 붙는 문자 집합 (기본값: `None`).
- **argument_default:** 인자의 전역 기본값 (기본값: `None`)
- **conflict_handler:** 충돌하는 선택 사항을 해결하기 위한 전략 (일반적으로 불필요함)
- **add_help:** 파서에 `-h/--help` 옵션을 추가 (기본값: `True`)
- **allow_abbrev:** 약어가 모호하지 않으면 긴 옵션을 축약할 수 있도록 함. (기본값: `True`)



#### add_argument() 메서드

- add_argument로 parser에 인자 추가
- 인자의 이름을 정할 때,  -h / --help 와 같이 약자와 fullname을 동시에 지정할 수 있음



##### 매개변수

- **name or flags** : 옵션 문자열의 이름이나 리스트

  - 인자 앞에 - 또는 --가 붙어 있는 경우 **선택형(optional) 인자** 붙어 있지 않은 경우에는 **위치형(positional) 인자**
    - 선택형 인자 : 필요할 때 입력해야 하는 인자(required = True 조건을 통해 필수로 입력하게 만들 수 있음)
    - 위치형 인자 : 필수로 입력해야 하는 인자
  - 인자가 여러가지 있을 경우, 위치형 인자는 순서를 꼭 지켜서 입력해야 하지만, optional 인자는 순서를 지키지 않아도 괜찮음

  

- **action** : 명령 행에서의 액션

  - store : 기본 action으로 인자 값을 저장함

  - store_const : 고정된 값을 저장할 때 사용

  - store_true : 값이 입력되면 True를 출력하고 아니면 False를 출력

  - store_false : 값이 입력되면 False를 출력하고 아니면 True를 출력
  - append : 여러 개의 값을 수집하여 리스트로 저장할 때 사용
  - append_const : 인자가 지정될 때마다 고정된 값을 리스트에 추가할 때 사용
  - count : 키워드 인자가 등장한 횟수를 계산함
  - help : 현재 파서의 모든 옵션에 대한 도움말 메시지를 출력
  - version : `version =` 키워드 인자를 입력하고 호출되면 버전 정보를 출력
  - extend : 리스트를 저장하고 각 인자 값으로 리스트 확장

- **nargs** : 소비되어야 하는 명령행 인자의 수

  - 일반적으로 하나의 명령행 인자를 하나의 액션과 결합
  - nargs 키워드 인자는 다른 수의 명령행 인자를 하나의 액션으로 연결할 수 있음

- **const**: 일부 action 및 nargs를 선택할 때 필요한 상수값.

- **default** : 인자가 명령행에 없고 namespace 객체에 없으면 생성되는 값

- **type** : 명령행 인자가 변환되어야 할 형
  
  - open 함수의 FileType 제공
- **choices**: 인자로 허용되는 값의 컨테이너
- **required**: 명령행 옵션을 생략 할 수 있는지 아닌지를 설정
- **help** : 인자가 하는 일에 대한 간단한 설명
- **metavar** : 사용 메시지에 사용되는 인자의 이름
- **dest** : parse_args() 가 반환하는 객체에 추가될 어트리뷰트의 이름



#### parse_args() 메서드

- parse_args()를 통해 parser 객체의 인자들 파싱







참고#1 : https://docs.python.org/ko/3/library/argparse.html#usage

참고#2 : https://wikidocs.net/73785

참고#3 : https://jayeon8282.tistory.com/6

 
