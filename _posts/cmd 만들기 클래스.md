## 📑 목차
- [소개](#소개)
- [클래스](#클래스)
- [클래스-내용](#클래스-내용)

---

# 소개
오늘은 cmd 클래스를 한번 만들어 봤습니다

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

내장 함수인 os 모듈을 정의하고 "sucmd" 라는 클래스를 생성합니다

```python

def __init__(self):
        self.value = ""

```
### __init__(self): 생성자 메서드
 
self.value 변수를 생성합니다

```python

    def value_input(self):
        self.value = input(os.getcwd() + ">")
        return self.value

```


