# Chapter 3: Functions

Funkcia je ako „mini-program“ vo vnútri veľkého programu. Jej hlavným účelom je zoskupiť kód, ktorý sa vykonáva viackrát, čím sa eliminuje duplicita kódu (tzv. deduplikácia kódu).

## 1. Definícia a volanie funkcie (Def & Call)

* **Definícia funkcie (`def`)** – Pomocou kľúčového slova `def`vytvárame novú funkciu. Kód pod týmto príkazom (odsadený) tvorí **telo funkcie**.
* **Volanie funkcie (Call)** – funkciu zavoláme jej menom s okrúhlymi zátvorkami.

```python
def hello():
    print("Howdy!")
    print("Hello there.")

hello()  # Volanie funkcie -> spustí oba printy
```

---

## 2. Parametre a argumenty (Parameters & Arguments)

* **Parameter** – Premenná napísaná v zátvorkách pri definícii funkcie. Slúži ako dočasné lokálne úložisko pre prichádzajúce dáta.
* **Argument** – Skutočná hodnota, ktorú odovzdávame do zátvoriek pri volaní funkcie. Táto hodnota sa automaticky priradí príslušnému parametru.

```python
def say_hello(name):  # 'name' je parameter
    print("Hello " + name)

say_hello("Alice")    # 'Alice' je argument
```

> **Poznámka:** Hodnota uložená v parametri sa po skončení funkcie automaticky vymaže.

---

## 3. Návratové hodnoty a príkaz `return`

Keď program zavolá funkciu, toto volanie sa vyhodnotí na určitú hodnotu. Táto hodnota sa nazýva **návratová hodnota**.

Vlastnú návratovú hodnotu definujeme pomocou kľúčového slova `return`.

Akonáhle Python narazí na príkaz `return`, okamžite ukončí vykonávanie funkcie a vráti výsledok späť na miesto, odkiaľ bola funkcia zavolaná.

### Hodnota `None`

* Predstavuje úplnú absenciu hodnoty.
* Píše sa vždy s veľkým **N**.
* Ak funkcia neobsahuje `return`, Python automaticky pridá:

```python
return None
```

Príklad:

```python
result = print("A")
print(result)   # None
```

---

## 4. Kľúčové argumenty (Keyword Arguments)

Okrem argumentov podľa poradia môžeme použiť aj argumenty podľa názvu.

### `end`

Určuje, čo sa vypíše na konci funkcie `print()`.

Predvolene:

```python
print("Hello")
print("World")
```

Výstup:

```
Hello
World
```

Bez nového riadku:

```python
print("Hello", end="")
print("World")
```

Výstup:

```
HelloWorld
```

### `sep`

Určuje oddeľovač medzi viacerými argumentmi.

```python
print("cats", "dogs", "mice", sep=", ")
```

Výstup:

```
cats, dogs, mice
```

---

## 5. Lokálny a globálny rozsah (Local and Global Scope)

Rozsah (**scope**) určuje, kde je premenná dostupná.

* Premenné vytvorené vo funkcii sú **lokálne**.
* Premenné vytvorené mimo funkcií sú **globálne**.

### Štyri základné pravidlá

1. Globálny kód nemôže pristupovať k lokálnym premenným.
2. Lokálny kód môže čítať globálne premenné.
3. Jedna funkcia nemôže používať lokálne premenné inej funkcie.
4. Lokálna a globálna premenná môžu mať rovnaký názov, ale ide o dve rôzne premenné. 

### Príkaz `global`

Ak chcete meniť globálnu premennú zvnútra funkcie:

```python
eggs = "global"

def spam():
    global eggs
    eggs = "spam"

spam()
print(eggs)    # spam
```

### Chyba `UnboundLocalError`

Ak vo funkcii najprv použijeme premennú a až neskôr jej priradíme hodnotu **bez použitia** `global`, Python automaticky predpokladá, že ide o **lokálnu premennú**. Keďže sa ju pokúša prečítať ešte pred jej vytvorením, program skončí chybou **`UnboundLocalError`**.

#### Nesprávny príklad

```python
eggs = "global"

def spam():
    print(eggs)      # Pokus o čítanie premennej
    eggs = "spam"    # Python ju považuje za lokálnu

spam()
```

**Výsledok:**

```text
UnboundLocalError: cannot access local variable 'eggs'
where it is not associated with a value
```

**Prečo vznikne chyba?**

Python pri preklade funkcie vidí priradenie:

```python
eggs = "spam"
```

Preto usúdi, že `eggs` je **lokálna premenná** v celej funkcii. Keď sa vykoná:

```python
print(eggs)
```

lokálna premenná ešte neexistuje, preto vznikne chyba.

#### Správne riešenie pomocou `global`

```python
eggs = "global"

def spam():
    global eggs
    print(eggs)      # Vypíše: global
    eggs = "spam"

spam()
print(eggs)          # Vypíše: spam
```

> **Zapamätaj si:** Ak vo funkcii priraďuješ hodnotu globálnej premennej, musíš použiť `global`, inak Python vytvorí novú lokálnu premennú s rovnakým názvom.

---

## 6. Spracovanie výnimiek (Exception Handling)

Ak počas vykonávania programu nastane chyba (**exception**), program štandardne skončí.

Pomocou blokov `try` a `except` môžeme chybu zachytiť.

* **`try`** – obsahuje kód, v ktorom môže vzniknúť chyba.
* **`except`** – vykoná sa iba v prípade, že nastane príslušná výnimka.

```python
def divide_by(number):
    try:
        return 42 / number
    except ZeroDivisionError:
        print("Chyba: Pokus o delenie nulou.")
        return None

print(divide_by(2))   # 21.0
print(divide_by(0))   # Chyba + None
```
