---
layout: post
---

## 📑 목차
- [소개](#소개)
- [클래스](#클래스)
- [클래스-내용](#클래스-내용)

---

# 소개
오늘은 cmd 클래스를 한번 만들어 봤습니다.

# 클래스
```python
import os
class sucmd:
    def __init__(self):
        self.value = ""

    def value_input(self):
        self.value = input(os.getcwd() + ">")
        return self.value

    def value_cd(self):
        try:
            if self.value[:2] == 'cd':

                if self.value[3:5] == '..':
                    os.chdir('..')
                else:
                    os.chdir(self.value[3:])
        except OSError:
            print("파일 이름, 디렉터리 이름 또는 볼륨 레이블 구문이 잘못되었습니다:")

    def value_dir(self):
        if self.value == 'dir':
            print(os.listdir('./'))

    def value_cat(self):
        if self.value[:3] == 'cat':
            self.value_open()

    def value_open(self):
        try:
            c = open(f"{self.value[4:]}", "r", encoding="utf-8")
            b = c.read()
            print(b)
            c.close()

        except FileNotFoundError:
            print(" 파일이 없습니다 ")

    def __str__(self):
        return self.value

def run():

    cmd = sucmd()

    while 1:

        cmd.value_input()

        cmd.value_dir()

        cmd.value_cd()

        cmd.value_cat()

if __name__ == "__main__":
    run()
```
# 클래스-내용
```python

import os
class sucmd:

```

내장 함수인 os 모듈을 정의하고 "sucmd" 라는 클래스를 생성합니다.

```python

def __init__(self):
        self.value = ""

```
### 메서드
self.value 변수를 생성합니다.

```python

    def value_input(self):
        self.value = input(os.getcwd() + ">")
        return self.value

```

콘솔에서 input 받은 값을 self.value 에 저장하고 현재디렉토리 위치를 리턴시키고 self.value를 리턴시키는 기능을 가진 메서드 입니다.

```python

    def value_cd(self):
        try:
            if self.value[:2] == 'cd':

                if self.value[3:5] == '..':
                    os.chdir('..')
                else:
                    os.chdir(self.value[3:])
        except OSError:
            print("파일 이름, 디렉터리 이름 또는 볼륨 레이블 구문이 잘못되었습니다:")


```

이 메서드는 self.value에 값의 2까지의 내용이 cd 라면 아랫코드를 수행합니다 만약 self.value에 값이 3부터 5까지의 내용이 .. 이라면 디렉토리의 위치를 부모폴더로 이동시키고 아니면 self.value에 3부터의 위치로 이동시킵니다.
만약 self.value값을 잘못입력해 OSError: 가 뜨면 예외처리 시킵니다.

```python

def value_dir(self):
        if self.value == 'dir':
            print(os.listdir('./'))

```

이 메서드는 만약  self.value값이 "dir"이라면 현 폴더에 있는 파일과 폴더 목록을 출력 시킵니다.

```python

  def value_cat(self):
        if self.value[:3] == 'cat':
            self.value_open()

```

이 메서드는  self.value값에 3번째까지에 내용이 cat이라면   self.value_open() 메서드를 실행시킵니다.

```python

    def value_open(self):
        try:
            c = open(f"{self.value[4:]}", "r", encoding="utf-8")
            b = c.read()
            print(b)
            c.close()

        except FileNotFoundError:
            print(" 파일이 없습니다 ")

```

이 메서드는 self.value에 4번째 부터의 값을 파일명으로 저장하고 utf-8 로 인코딩해 열기모드로 실행합니다 또한 b 에 c = 파일내용을 저장하고 프린트합니다 그리고 파일을 닫습니다
만약 현재위치한 폴더안에 해당된 파일이 없어 FileNotFoundError: 가 뜨면 예외처리 시킵니다

```python

   def __str__(self):
        return self.value

```

원래 클래스에서 리턴을 시키며는 메모리주소값이 리턴되게 됩니다 그 이유는 원래 모든 클래스에 부모는 오브젝트 클래스입니다 그곳에 있는 __str__ 메서드는 값이 출력되거나 리턴받을때 자동으로 실행됩니다 그렇기 떄문에 제가 만든 클래스 에서 __str__메서드를 생성하면 오브젝트 클래스에 있는 __str__ 메서드가 동작하지 않고 제가 만든 클래스에 있는 __str__ 메서드가 동작하기 떄문에 value_input() 메서드에서 self.value 리턴 시킬때 메모리주소 말고 input받은 값이 리턴되게 됩니다.

```python

def run():

    cmd = sucmd()

    while 1:

        cmd.value_input()

        cmd.value_dir()

        cmd.value_cd()

        cmd.value_cat()

if __name__ == "__main__":
    run()

```

프로그램이 시작되면 자동으로   run()  함수를 실행시키고 cmd변수에 sucmd() 클래스르 정의 합니다 그리고 반복문을 돌려 메서드들을 실행시킵니다

