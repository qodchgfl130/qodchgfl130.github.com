---
layout: post
---

# Language Test

## Python
```python
class Character:

    def __init__(self,name, hp, at, de):
        self.name = name
        self.hp = hp
        self.at = at
        self.de = de

    def info(self):
        print(f"{self.name} 체력{self.hp} 공격력{self.at} 방어력{self.de}")

    def attack(self,대상):
        print(f"{self.name}이 {대상.name}을 공격했습니다")
        대상.damage(self.at)

    def damage(self,damage1):
        self.hp -= (damage1 - self.de)
        if self.hp >= 0:
            print(f"{self.name} 남은체력{self.hp}")
        else:
            self.hp = 0
            print(f"{self.name} 남은체력{self.hp}으로 죽었습니다")

    def has_weapon(self,weapon):
        self.weapon = weapon
        self.at += weapon.up_at
        print(f"{self.name}이(가) {weapon.name}을(를) 장착했습니다! 공격력 +{weapon.up_at}")

    def has_armor(self,armor):
        self.armor = armor
        self.de += armor.up_de
        print(f"{self.name}이(가) {armor.name}을(를) 장착했습니다! 방어력 +{armor.up_de}")

class Player(Character):
    pass

class enemy(Character):
    pass

class Weapon:
    def __init__(self,name,up_at):
        self.name = name
        self.up_at = up_at
class armor:
    def __init__(self,name,up_de):
        self.name = name
        self.up_de = up_de

a = Player("김수현",100, 10, 20)
b = enemy("몬스터",80, 15, 5)

sword=Weapon("sword",50)
long_sword=Weapon("long sword",60)

steel_armor=armor("steel armor",30)
diamond_armor=armor("diamond armor",80)


a.has_armor(steel_armor)
a.has_weapon(sword)


a.info()
b.info()

a.attack(b)

a.info()
b.info()

a.attack(b)
```


