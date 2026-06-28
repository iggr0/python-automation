# Chapter 2: Flow Control

## 1. Pravdivostné hodnoty (Boolean Values)
Zatiaľ čo dátové typy ako `int` alebo `str` majú nekonečne veľa hodnôt, dátový typ **Boolean** má iba dve:
* **`True`** (Pravda)
* **`False`** (Nepravda)

*Pozor:* Musia sa písať vždy s veľkým počiatočným písmenom a bez úvodzoviek. `true` (s malým) v Pythone neexistuje a `'True'` (v úvodzovkách) je obyčajný text (`str`).

## 2. Relačné / Porovnávacie operátory (Comparison Operators)
Porovnávajú dve hodnoty a vyhodnotia sa na jednu Boolean hodnotu (`True` alebo `False`).

| Operátor | Význam | Príklad | Výsledok |
| :---: | :--- | :--- | :--- |
| `==` | Rovná sa | `42 == 42` <br> `42 == '42'` | `True` <br> `False` |
| `!=` | Nerovná sa | `2 != 3` | `True` |
| `<` | Menší ako | `5 < 4` | `False` |
| `>` | Väčší ako | `6 > 2` | `True` |
| `<=` | Menší alebo rovný | `4 <= 4` | `True` |
| `>=` | Väčší alebo rovný | `3 >= 5` | `False` |

*Dôležité:* Operátor `==` (porovnanie) je niečo úplne iné ako `=` (priradenie hodnoty do premennej). Celé číslo sa nikdy nerovná reťazcu (textu), preto `42 == '42'` je `False`.

## 3. Logické operátory (Boolean Operators)

Používajú sa na kombinovanie viacerých Boolean hodnôt alebo podmienok.

* **`and` (A zároveň):** Výsledok je `True` **iba vtedy**, ak sú obe podmienky pravdivé.
  ```python
  (4 < 5) and (5 < 6)
  # True

  (4 < 5) and (6 < 5)
  # False
  ```

* **`or` (ALEBO):** Výsledok je `True`, ak je pravdivá **aspoň jedna** podmienka.
  ```python
  (4 < 5) or (6 < 5)
  # True

  (5 > 8) or (3 > 7)
  # False
  ```

* **`not` (Negácia):** Obráti Boolean hodnotu na opačnú.
  ```python
  not True
  # False

  not (5 > 3)
  # False
  ```

## 4. Príkaz `if`

Príkaz `if` vykoná blok kódu iba vtedy, ak je podmienka `True`.

```python
age = 20

if age >= 18:
    print("Adult")
```

## 5. Príkaz `else`

Blok `else` sa vykoná, ak podmienka v `if` nie je splnená.

```python
age = 16

if age >= 18:
    print("Adult")
else:
    print("Minor")
```

## 6. Príkaz `elif`

Používa sa na kontrolu viacerých podmienok.

```python
score = 85

if score >= 90:
    print("A")
elif score >= 80:
    print("B")
else:
    print("C")
```

> Python kontroluje podmienky zhora nadol. Vykoná iba prvú pravdivú podmienku.

## 7. Odsadenie (Indentation)

Python používa odsadenie na označenie blokov kódu.

Správne:

```python
if x > 0:
    print("Positive")
```

Nesprávne:

```python
if x > 0:
print("Positive")
```

## 8. Truthy a Falsy hodnoty

V podmienkach Python automaticky považuje niektoré hodnoty za `False`.

```python
False
None
0
0.0
''
[]
{}
()
```

Všetky ostatné hodnoty sú považované za `True`.

Príklad:

```python
name = ""

if name:
    print("Name exists")
else:
    print("Empty")
```

## 9. Najčastejšie chyby

Použitie `=` namiesto `==`

```python
if age = 18:
```

Správne:

```python
if age == 18:
```

---

Zabudnutá dvojbodka

```python
if age > 18
```

Správne:

```python
if age > 18:
```

---

Nesprávne odsadenie

```python
if age > 18:
print("Adult")
```

Správne:

```python
if age > 18:
    print("Adult")
```
  