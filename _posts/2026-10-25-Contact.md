# 파이썬으로 연락처 관리 프로그램 만들기

## 1. 프로젝트 소개

파이썬을 공부하면서 연락처를 추가하고, 검색하고, 삭제할 수 있는 **콘솔 기반 연락처 관리 프로그램**을 만들어 보았다.

이번 프로젝트에서는 파이썬의 클래스와 메서드, 리스트, 반복문, 조건문, 정규식 등을 활용했다.

### 구현한 기능

| 명령어 | 기능 |
|---|---|
| `add` | 새로운 연락처 추가 |
| `search` | 이름으로 연락처 검색 |
| `list` | 전체 연락처 출력 |
| `delete` | 이름과 전화번호를 이용해 연락처 삭제 |
| `save` | 연락처 저장 기능 (구현 예정) |
| `help` | 사용 가능한 명령어 출력 |
| `exit` | 프로그램 종료 |

---

## 2. 클래스와 메서드로 프로그램 구성하기

프로그램은 `Contact`라는 클래스를 중심으로 구성했다.

```python
class Contact:
    def __init__(self):
        self.email = None
        self.number = None
        self.name = None

        self.contactlist = [
            ['김수현', '1', '1'],
            ['안현지', '1', '1'],
            ['김수광', '1', '1'],
            ['김현지', '1', '1']
        ]
```

### `__init__()`이란?

`__init__()`은 객체가 생성될 때 자동으로 실행되는 초기화 메서드다.

이 메서드에서는 연락처를 입력받을 때 사용할 변수와 연락처 목록을 초기화했다.

### `self`란?

`self`는 현재 객체 자신을 가리킨다.

예를 들어 `self.contactlist`는 해당 객체가 사용하는 연락처 목록을 의미한다. 클래스 내부의 여러 메서드에서 같은 연락처 목록을 사용하기 위해 `self`를 활용했다.

### 리스트로 연락처 관리하기

연락처 하나를 다음과 같은 리스트로 표현했다.

```python
['김수현', '01012345678', 'example@gmail.com']
```

각 항목의 위치는 다음과 같다.

- `contact[0]`: 이름
- `contact[1]`: 전화번호
- `contact[2]`: 이메일

여러 연락처를 하나의 리스트에 저장해 관리했다.

---

## 3. 이메일 정규식 검사하기

이번 프로젝트에서 새롭게 활용한 기능은 **정규식(Regular Expression, Regex)** 이다.

정규식은 문자열이 특정한 패턴이나 규칙에 일치하는지 검사하거나, 문자열에서 원하는 부분을 찾고 바꾸는 데 사용하는 표현식이다.

내가 만든 프로그램에서는 이메일을 입력받은 후, 입력한 문자열이 내가 설정한 이메일 형식에 맞는지 검사하도록 구현했다.

### 3-1. 정규식 코드

```python
import re

def CheckEmail(self, email):
    pattern = r"^[a-zA-Z0-9]+@[a-zA-Z]+\.[a-zA-Z]{2,}$"

    if re.fullmatch(pattern, email):
        return True
    else:
        return False
```

여기서 `re`는 파이썬에서 정규식을 사용하기 위한 모듈이다.

`re.fullmatch()`는 입력한 문자열 전체가 정규식 패턴과 일치하는지 검사한다.

- 패턴과 일치하면 일치 객체를 반환한다.
- 일치하지 않으면 `None`을 반환한다.

따라서 조건문에서 정규식 검사 결과를 확인하고, 이메일 형식이 맞으면 `True`, 맞지 않으면 `False`를 반환하도록 만들었다.

### 3-2. 정규식 패턴 분석하기

사용한 정규식은 다음과 같다.

```python
r"^[a-zA-Z0-9]+@[a-zA-Z]+\.[a-zA-Z]{2,}$"
```

각 기호와 표현의 의미는 다음과 같다.

| 표현 | 의미 |
|---|---|
| `r"..."` | 문자열을 정규식 패턴으로 작성할 때 사용하는 Raw String |
| `^` | 문자열의 시작 |
| `[a-zA-Z0-9]` | 영문 대문자, 영문 소문자 또는 숫자 |
| `+` | 앞의 패턴이 한 번 이상 반복됨 |
| `@` | 문자 `@` |
| `[a-zA-Z]+` | 영문 대소문자가 한 번 이상 반복됨 |
| `\.` | 정규식에서 특별한 의미를 가진 점이 아니라 실제 마침표 `.` |
| `[a-zA-Z]{2,}` | 영문자가 최소 두 번 반복됨 |
| `$` | 문자열의 끝 |

이 패턴은 다음과 같은 구조의 문자열을 검사한다.

**영문자와 숫자 + @ + 영문자 + 마침표 + 두 글자 이상의 영문자**

예를 들어 다음과 같은 입력은 패턴에 일치한다.

```text
abc123@gmail.com
hello@naver.com
user@test.kr
```

반면 다음과 같은 입력은 일치하지 않는다.

```text
abc123gmail.com  # @가 없음
hello@123.com    # @ 뒤에 영문자가 없음
user@test.c      # 마침표 뒤의 영문자가 한 글자뿐임
```

단, 이 정규식은 이메일 형식을 간단하게 검사하기 위해 만든 것이다. 실제 이메일 주소에서 허용되는 모든 형식을 지원하지는 않는다.

또한 **정규식 검사를 통과했다고 해서 실제로 존재하는 이메일 주소라는 뜻은 아니다.** 입력한 문자열이 설정한 형식에 맞는지만 확인할 수 있다.

---

## 4. 연락처 추가 기능 구현하기

연락처를 추가하는 `Add()` 메서드에서는 이메일, 전화번호, 이름을 입력받도록 만들었다.

```python
def Add(self):
    self.email = input('이메일 :')

    if not self.CheckEmail(self.email):
        print(f"'{self.email}'은(는) 올바른 이메일 형식이 아닙니다")
        return

    self.number = input('전화번호 :')
    self.name = input('이름 :')

    if self.number == '' or self.name == '':
        print('연락처 등록에 실패하였습니다.')
        return
    else:
        print(self.name + '님을 연락처에 추가했습니다')
        self.InputAdd()
```

### 코드 실행 순서

1. 사용자에게 이메일을 입력받는다.
2. `CheckEmail()`을 호출해 이메일 형식을 검사한다.
3. 이메일 형식이 올바르지 않으면 오류 메시지를 출력하고 메서드를 종료한다.
4. 이메일 형식이 올바르면 전화번호와 이름을 입력받는다.
5. 전화번호나 이름이 비어 있다면 등록에 실패한다.
6. 모든 입력이 올바르면 `InputAdd()`를 호출해 연락처 목록에 추가한다.

여기서 `return`은 현재 실행 중인 메서드를 종료하는 역할을 한다.

이메일 형식이 잘못되었을 때 `return`을 사용하면 이후의 입력 과정이 실행되지 않는다.

---

## 5. 연락처 목록에 데이터 추가하기

실제로 연락처 목록에 데이터를 추가하는 부분은 `InputAdd()` 메서드다.

```python
def InputAdd(self):
    self.contactlist.append([
        self.name,
        self.number,
        self.email
    ])
```

`append()`는 리스트의 마지막에 새로운 항목을 추가하는 메서드다.

이 코드는 사용자가 입력한 이름, 전화번호, 이메일을 하나의 리스트로 묶어 기존 연락처 목록에 추가한다.

예를 들어 다음과 같은 정보를 입력했다고 가정하자.

```text
이메일 : example@gmail.com
전화번호 : 01012345678
이름 : 홍길동
```

그러면 연락처 목록에 다음과 같은 데이터가 추가된다.

```python
['홍길동', '01012345678', 'example@gmail.com']
```

---

## 6. 이름으로 연락처 검색하기

`Search()` 메서드에서는 사용자가 입력한 문자열이 연락처의 이름에 포함되어 있는지 검사한다.

```python
def Search(self):
    number = 0
    name = []
    search = input('검색할 이름 일부:')

    for contact in range(len(self.contactlist)):
        if search in self.contactlist[contact][0]:
            number = number + 1
            name.append(self.contactlist[contact][0])

    print(search, '검색결과', number, '건')

    for a in range(len(name)):
        print(name[a])
```

### 핵심 개념

**`len()`**

리스트에 들어 있는 항목의 개수를 반환한다.

**`range()`**

반복문에서 사용할 숫자의 범위를 생성한다.

**`in`**

특정 문자열이나 값이 다른 문자열 또는 자료에 포함되어 있는지 검사한다.

예를 들어 연락처에 `김수현`이 저장되어 있다면 `김수`를 검색해도 결과에 포함된다.

검색된 이름은 `name` 리스트에 저장하고, 검색 결과의 개수는 `number` 변수에 기록한다.

---

## 7. 연락처 삭제하기

`Delete()` 메서드에서는 이름과 전화번호를 입력받아 연락처를 삭제한다.

```python
def Delete(self):
    delete = []

    search = input('삭제할 연락처 이름.')
    delete.append(search)

    search = input('삭제할 연락처 전화번호.')
    delete.append(search)

    for contact in range(len(self.contactlist)):
        if (
            delete[0] in self.contactlist[contact][0]
            and delete[1] == self.contactlist[contact][1]
        ):
            del self.contactlist[contact]
            print('성공적으로 연락처를 삭제했습니다.')
            self.List()
            return

    print('존재하지 않는 연락처입니다.')
```

### 핵심 개념

**`and`**

두 조건이 모두 참일 때 전체 조건이 참이 된다.

**`del`**

리스트의 특정 항목을 삭제할 때 사용한다.

**`return`**

연락처를 삭제한 뒤 메서드를 종료한다.

이 코드는 이름이 입력한 문자열을 포함하고 전화번호가 정확히 일치하는 연락처를 삭제한다.

다만 현재 이름 비교는 `in`을 사용하므로 부분적으로 일치하는 이름도 검색된다. 정확히 같은 이름만 삭제하고 싶다면 다음처럼 `==`를 사용하면 된다.

```python
delete[0] == self.contactlist[contact][0]
```

---

## 8. 프로그램 실행과 명령어 처리하기

`Main()` 메서드에서는 반복문과 조건문을 이용해 사용자가 입력한 명령어에 따라 서로 다른 메서드를 실행하도록 만들었다.

```python
def Main(self):
    print("=" * 42)
    print(" 연락처 관리 프로그램")
    print("=" * 42)

    while True:
        search = input('>>>')

        if search == 'add':
            self.Add()
        elif search == 'search':
            self.Search()
        elif search == 'list':
            self.List()
        elif search == 'delete':
            self.Delete()
        elif search == 'save':
            self.Save()
        elif search == 'help':
            self.Help()
        elif search == 'exit':
            self.Exit()
        else:
            print(f"'{search}'은(는) 실행할 수 없는 명령어입니다.")
```

`while True`는 조건이 항상 참이므로 반복문을 계속 실행한다.

사용자가 `exit`를 입력하면 `Exit()` 메서드가 실행되고, `sys.exit()`를 통해 프로그램을 종료한다.

이러한 구조를 이용하면 프로그램이 종료되기 전까지 여러 명령어를 반복해서 입력할 수 있다.

---

## 9. 프로젝트를 만들며 배운 점

이번 프로젝트를 만들면서 파이썬의 여러 기능을 실제 프로그램에 적용해 보았다.

특히 정규식을 사용해 입력값이 특정 규칙에 맞는지 검사하는 방법을 배웠다.

**정규식은 입력한 문자열이 내가 설정한 규칙과 일치하는지 검사하는 도구다.** 이를 활용하면 이메일처럼 일정한 형식이 있는 문자열을 검사할 수 있다.

또한 클래스와 메서드를 이용해 기능을 나누고, 리스트에 데이터를 저장하며, 반복문과 조건문으로 사용자의 입력에 따라 프로그램이 다르게 작동하도록 만들었다.

아직 연락처 저장 기능은 구현하지 않았지만, 앞으로 JSON을 활용해 프로그램을 종료한 뒤에도 연락처가 유지되도록 개선할 계획이다.

이번 프로젝트를 통해 단순히 파이썬 문법을 익히는 것을 넘어, 여러 문법을 조합해 실제로 작동하는 프로그램을 만드는 경험을 쌓을 수 있었다.
