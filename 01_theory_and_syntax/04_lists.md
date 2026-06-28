# Chapter 3: Lists

Zoznam (`list`) je **usporiadaná, meniteľná sekvenčná dátová štruktúra**, ktorá umožňuje uchovávať ľubovoľný počet objektov. Na rozdiel od klasických polí nemá pevnú veľkosť – Python ju automaticky prispôsobuje podľa potreby pri pridávaní alebo odoberaní prvkov.

---

## 1. Ako to funguje vnútri?

Python implementuje zoznam (`list`) ako **dynamické pole**, ktoré obsahuje **referencie na objekty**, nie samotné objekty. To znamená, že zoznam neukladá hodnoty priamo, ale odkazy na objekty v pamäti, vďaka čomu môže obsahovať prvky rôznych dátových typov.

Pri vytvorení zoznamu Python zvyčajne alokuje o niečo viac pamäte, ako je aktuálne potrebné (tzv. **over-allocation**). Vďaka tomu je pridávanie prvkov pomocou metódy `.append()` vo väčšine prípadov veľmi rýchle.

Ak sa vyhradená kapacita zaplní, Python vytvorí väčšie pole, skopíruje doň všetky existujúce referencie a pôvodné pole uvoľní. Táto operácia je časovo náročnejšia.

> **Poznámka**
>
> Metóda `.append()` má **amortizovanú časovú zložitosť `O(1)`**.
>
> Väčšina volaní prebehne v konštantnom čase (`O(1)`), pretože Python využíva už alokovanú voľnú kapacitu. Len občas musí vytvoriť väčšie pole a presunúť všetky referencie (`O(n)`). Keďže sa to deje len zriedkavo, priemerná časová zložitosť zostáva **amortizovane `O(1)`**.

>
> `append()` → **amortizované `O(1)`**

---

## 2. Pokročilé indexovanie a Slicing (Rezy)

Základné pravidlá:

* `animals[0]` je prvý prvok.
* `animals[-1]` je posledný prvok.
* Prístup mimo rozsahu vyhodí výnimku `IndexError`.

### Slicing (`[start:stop:step]`)

**Slicing nikdy nevyhodí `IndexError`**, aj keď zadáš indexy mimo rozsahu zoznamu. Python ich automaticky upraví na najbližší platný rozsah.

```python
a = [0, 1, 2, 3, 4, 5]

print(a[2:100])     # [2, 3, 4, 5]
print(a[10:20])     # []
print(a[-100:3])    # [0, 1, 2]
```

### Chyták s parametrom `step`

* Ak je `step` kladný, zoznam sa prechádza **zľava doprava**.

  * Ak je `start >= stop`, výsledkom je prázdny zoznam.
* Ak je `step` záporný, zoznam sa prechádza **sprava doľava**.

  * Ak je `start <= stop`, výsledkom je prázdny zoznam.
* `a[::-1]` vytvorí **novú obrátenú kópiu** zoznamu.

---

## 3. Deštruktívne vs. nedeštruktívne operácie

Pri práci so zoznamami je dôležité rozlišovať, či operácia:

* **mení pôvodný objekt** (*in-place*),
* alebo vytvorí **nový objekt**.

### A. Odstraňovanie prvkov

#### `del`

```python
del a[index]
```

* odstráni prvok na zadanom indexe,
* je to **kľúčové slovo**, nie metóda,
* nemá návratovú hodnotu.

---

#### `pop()`

```python
a.pop(index)
```

* odstráni prvok,
* vráti odstránenú hodnotu,
* bez argumentu odstráni posledný prvok.

---

#### `remove()`

```python
a.remove(value)
```

* odstráni prvý výskyt hodnoty,
* ak sa hodnota nenachádza v zozname, vyhodí `ValueError`.

---

#### `clear()`

```python
a.clear()
```

* odstráni všetky prvky zo zoznamu,
* výsledkom je prázdny zoznam.

---

### B. Pridávanie prvkov

#### `append()`

Pridá jeden nový prvok na koniec zoznamu.

```python
a.append(5)
```

---

#### `extend()`

Pridá všetky prvky z iterovateľného objektu.

```python
a.extend([4, 5, 6])
```

---

#### `insert()`

```python
a.insert(index, value)
```

Vloží prvok na zadanú pozíciu.

```python
a = [1, 2, 3]

a.insert(1, 100)

print(a)
# [1, 100, 2, 3]
```

> **Poznámka**
>
> `insert()` má časovú zložitosť **O(n)**, pretože Python musí posunúť všetky nasledujúce prvky.

---

### C. `sort()` vs. `sorted()`

#### `sort()`

```python
a.sort()
```

* zoradí pôvodný zoznam,
* vracia `None`.

#### `sorted()`

```python
sorted(a)
```

* vytvorí nový zoradený zoznam,
* pôvodný zostáva nezmenený.

> **Chyták**

```python
my_list = [3, 1, 2]

sorted_list = my_list.sort()

print(sorted_list)
# None
```

---

### D. `reverse()` vs. `[::-1]`

#### `reverse()`

```python
a.reverse()
```

* otočí pôvodný zoznam (*in-place*).

#### `[::-1]`

```python
b = a[::-1]
```

* vytvorí novú otočenú kópiu.

---

## 4. `append()` vs. `extend()` vs. operátor `+`

### `append()`

```python
a = [1, 2]
a.append([3, 4])

# [1, 2, [3, 4]]
```

Pridá objekt ako **jeden prvok**.

---

### `extend()`

```python
a = [1, 2]
a.extend([3, 4])

# [1, 2, 3, 4]
```

Rozbalí iterovateľný objekt a pridá všetky jeho prvky.

> **Chyták**

```python
a = [1, 2]

a.extend("XYZ")

print(a)
# [1, 2, 'X', 'Y', 'Z']
```

---

### Operátor `+`

```python
c = a + b
```

* vytvorí nový zoznam,
* pôvodné zoznamy nemení.

---

## 5. Referencie, plytká a hlboká kópia

### Priradenie

```python
b = a
```

Nevytvára nový zoznam.

Obe premenné ukazujú na ten istý objekt.

---

### Plytká kópia

```python
b = a.copy()

# alebo

b = a[:]
```

Vytvorí nový zoznam, ale vnorené objekty zostávajú spoločné.

```python
a = [[1, 2], [3, 4]]

b = a.copy()

b[0][0] = 999

print(a)
# [[999, 2], [3, 4]]
```

---

### Hlboká kópia

```python
import copy

b = copy.deepcopy(a)
```

Rekurzívne vytvorí kópiu všetkých vnorených objektov.

---

## 6. Iterácia cez zoznam

Najčastejšie spôsoby prechádzania zoznamu.

```python
for item in my_list:
    print(item)
```

Ak potrebujeme aj index:

```python
for index, value in enumerate(my_list):
    print(index, value)
```

---

## 7. List Comprehension

Elegantný spôsob vytvárania nových zoznamov.

```python
squares = [x**2 for x in range(10)]
```

S podmienkou:

```python
evens = [x for x in numbers if x % 2 == 0]
```

---

## 8. Efektivita a časová zložitosť

### `pop()` vs. `pop(0)`

* `pop()` → **O(1)**
* `pop(0)` → **O(n)**

---

### Operátor `in`

```python
x in my_list
```

Vyhľadáva lineárne.

Časová zložitosť:

```text
O(n)
```

---

### `len()`

```python
len(my_list)
```

Časová zložitosť:

```text
O(1)
```

---

## 9. Najčastejšie chyby

### Mutovanie počas iterácie

```python
for x in numbers:
    numbers.remove(x)
```

Prvky sa môžu preskočiť.

Správne:

```python
for x in numbers[:]:
    ...
```

alebo použiť **List Comprehension**.

---

### Predvolený mutovateľný argument

```python
def add_to(x, target=[]):
    target.append(x)
```

Správne:

```python
def add_to(x, target=None):
    if target is None:
        target = []

    target.append(x)
```

---

### Násobenie vnorených zoznamov

```python
matrix = [[0] * 3] * 3

matrix[0][0] = 1

print(matrix)
# [[1,0,0],[1,0,0],[1,0,0]]
```

> **Chyták**
>
> Nevytvorili sa tri nezávislé zoznamy, ale tri referencie na ten istý vnorený zoznam.

---

## 10. Časová zložitosť najčastejších operácií

| Operácia    | Zložitosť           |
| ----------- | ------------------- |
| `append()`  | amortizované `O(1)` |
| `pop()`     | `O(1)`              |
| `pop(0)`    | `O(n)`              |
| `insert()`  | `O(n)`              |
| `remove()`  | `O(n)`              |
| `x in list` | `O(n)`              |
| `len()`     | `O(1)`              |
| `copy()`    | `O(n)`              |
| `sort()`    | `O(n log n)`        |

---

## 11. Rýchle porovnanie: `list` vs. `tuple`

| Vlastnosť          | `list`             | `tuple`                                                  |
| ------------------ | ------------------ | -------------------------------------------------------- |
| Mutabilita         | Mutable            | Immutable                                                |
| Syntax             | `[1,2,3]`          | `(1,2,3)`                                                |
| Jednoprvkový zápis | —                  | `(1,)`                                                   |
| Pamäť              | Vyššia réžia       | Menšia réžia                                             |
| Rýchlosť           | O niečo pomalší    | O niečo rýchlejší                                        |
| Hashovateľný       | x                  |  (ak obsahuje iba immutable objekty)                    |
| Použitie           | Meniteľné kolekcie | Fixné záznamy, návratové hodnoty funkcií, kľúče v `dict` |
