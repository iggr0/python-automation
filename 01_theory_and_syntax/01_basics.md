# Chapter 1: Python Basics

## 1. Expressions & Operators

### Prehľad operátorov (od najvyššej priority):
| Operátor | Operácia | Príklad | Výsledok |
| :---: | :--- | :--- | :--- |
| `**` | Exponent / Mocnina | `2 ** 3` | `8` |
| `%` | Modulo (Zvyšok po delení) | `22 % 8` | `6` |
| `//` | Celočíselné delenie (Zaokrúhlené nadol) | `22 // 8` | `2` |
| `/` | Klasické delenie | `22 / 8` | `2.75` |
| `*` | Násobenie | `3 * 5` | `15` |
| `-` | Odčítanie | `5 - 2` | `3` |
| `+` | Sčítanie | `2 + 2` | `4` |

*Chyba syntaxe (`SyntaxError`):* Nastane, ak výraz napíšete gramaticky nesprávne (napr. `5 + `).

## 2. Data Types
Každá hodnota v Pythone patrí presne do jedného dátového typu:
1. **Celé čísla (`int`):** Čísla bez desatinnej čiarky (napr. `42`, `-5`).
2. **Desatinné čísla (`float`):** Čísla s desatinnou čiarkou (napr. `3.14`, `10.0`).
3. **Reťazce (`str`):** Textové hodnoty ohraničené jednoduchými úvodzovkami `'` (napr. `'Hello'`).

## 3. String Operations
Význam operátorov sa mení podľa toho, s akým dátovým typom pracujú:
* **String Concatenation (Spájanie textu):** Operátor `+` spojí dva reťazce dokopy.
  ```python
  'Alice' + 'Bob'  # Výsledok: 'AliceBob'

## 4. Comments

Jednoriadkový:

``` python
# Toto je komentár
```
Viacriadkový:

``` python
"""
Viacriadkový komentár
"""
```
## 5. Variables

Premenné sa vytvárajú priradením pomocou operátora `=`. Python typ určí automaticky.

```python
x = 10
pi = 3.14
name = "Peter"
```
Premenná môže neskôr obsahovať aj hodnotu iného typu.

```python
x = 10
x = "Hello"
```
## 6. Type Casting

* **str():** Skonvertuje hodnotu na reťazec (napr. str(29) vytvorí '29').

* **int():** Skonvertuje hodnotu na celé číslo. Ak jej odovzdáte float, odstrihne desatinnou časť (napr. int(7.7) vráti 7).

* **float():** Skonvertuje hodnotu na desatinné číslo (napr. float(10) vytvorí 10.0).

Upozornenie: Konverzia textu, ktorý neobsahuje číslo (napr. int('hello')), vyhodí chybu ValueError.