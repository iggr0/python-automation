# Chapter 6 – Manipulating Strings

# 1. String Data Type

String (`str`) je základný dátový typ určený na reprezentáciu textových údajov. Prakticky každá aplikácia, s ktorou sa stretneš, pracuje so stringami – od jednoduchého mena používateľa až po komunikáciu medzi servermi alebo vstupy pre modely umelej inteligencie.

Na rozdiel od čísel, ktoré reprezentujú kvantitatívne údaje, string reprezentuje **sekvenciu znakov**. Každý znak je uložený podľa štandardu **Unicode**, vďaka čomu Python podporuje väčšinu svetových jazykov vrátane slovenčiny.

String je **objekt**. To znamená, že okrem samotných znakov obsahuje aj množstvo vstavaných metód, pomocou ktorých možno text spracovávať.

Najdôležitejšie vlastnosti stringu:

* je usporiadanou sekvenciou znakov,
* podporuje indexovanie a slicing,
* je immutable (nemenný),
* podporuje množstvo vstavaných metód,
* používa Unicode.

Na rozdiel od niektorých jazykov Python **nemá samostatný dátový typ `char`**. Jeden znak je jednoducho string dĺžky 1.

### Príklad

```python
text = "Python" # string dlzky 6
```

---

# 2. Ako Python reprezentuje String

Keď vytvoríš string:

```python
name = "Python"
```

Python nevytvorí iba šesť znakov vedľa seba v pamäti. Vytvorí objekt, ktorý obsahuje:

* samotné Unicode znaky,
* informáciu o dĺžke,
* typ objektu,
* hash hodnotu (využívanú napr. v dictionary),
* odkazy na vstavané metódy.

To vysvetľuje, prečo môžeme písať:

```python
name.upper()
```

Metóda `upper()` nie je samostatná funkcia, ale metóda objektu typu `str`.

Ďalšou dôležitou vlastnosťou je **immutability**. Keďže Python pozná presnú dĺžku a obsah stringu už pri jeho vytvorení, môže optimalizovať prácu s pamäťou a bezpečne používať stringy ako kľúče v slovníkoch.

Táto vlastnosť zároveň znamená, že ak "zmeníme" string, v skutočnosti vzniká **nový objekt**.

---

# 3. String Literals

String literal je spôsob zápisu textu priamo v zdrojovom kóde.

Python podporuje viacero spôsobov zápisu:

* jednoduché úvodzovky `'...'`,
* dvojité úvodzovky `"..."`,
* trojité úvodzovky `'''...'''` alebo `"""..."""`.

Jednoduché aj dvojité úvodzovky sú rovnocenné. Výber závisí najmä od čitateľnosti.

### Escape sekvencie

Niektoré znaky nemožno zapísať priamo. Používajú sa tzv. **escape sekvencie**, ktoré začínajú spätným lomítkom (`\`).

Najčastejšie:

| Sekvencia | Význam               |
| --------- | -------------------- |
| `\n`      | nový riadok          |
| `\t`      | tabulátor            |
| `\\`      | spätné lomítko       |
| `\"`      | dvojité úvodzovky    |
| `\'`      | jednoduché úvodzovky |

Escape sekvencie umožňujú zapisovať špeciálne znaky bez narušenia syntaxe programu.

### Raw Strings

Pri práci s cestami k súborom alebo regulárnymi výrazmi sa používa **Raw String**.

Pri raw stringu Python escape sekvencie nespracováva.

To je veľmi užitočné napríklad pri Windows cestách alebo regulárnych výrazoch.

### Multiline Strings

Pomocou trojitých úvodzoviek možno zapisovať text na viac riadkov.

Používa sa pri:

* dokumentácii funkcií,
* SQL príkazoch,
* HTML šablónach,
* dlhých textoch.

### Príklad

```python
message = """Toto je
viacriadkový
text."""
```

---

# 4. Indexing and Slicing

Keďže string predstavuje usporiadanú sekvenciu znakov, ku každému znaku možno pristupovať pomocou indexu.

Prvý znak má index **0**.

Posledný znak možno získať aj pomocou záporného indexu.

To umožňuje pristupovať ku koncu stringu bez znalosti jeho dĺžky.

### Indexovanie

Indexovanie vracia **jeden znak**.

Je to veľmi rýchla operácia, pretože Python presne pozná adresu každého znaku.

### Slicing

Slicing slúži na získanie časti stringu.

Na rozdiel od indexovania vracia nový string obsahujúci požadovaný rozsah znakov.

Dôležité pravidlá:

* začiatočný index je zahrnutý,
* koncový index sa nezapočítava,
* výsledkom je nový objekt.

Slicing nikdy nemení pôvodný string.

### Prečo slicing vytvára nový objekt?

Dôvodom je immutable povaha stringov.

Keďže pôvodný objekt nemožno meniť, Python vytvorí nový objekt obsahujúci iba požadovanú časť textu.

To zaručuje bezpečnosť práce s dátami a umožňuje efektívnejšiu správu pamäte.

### Príklad

```python
word = "Programming"

print(word[0])      # P
print(word[:7])     # Program
```

---

# 5. Immutable Strings

Toto je najdôležitejší koncept celej kapitoly.

**Immutable** znamená, že po vytvorení objektu už nemožno meniť jeho obsah.

Pri stringoch to znamená, že jednotlivé znaky nemožno prepísať.

Ak program potrebuje text upraviť, Python vytvorí nový objekt a pôvodný ponechá nezmenený.

Táto vlastnosť má niekoľko významných výhod.

## Bezpečnosť

Ak dve premenné odkazujú na ten istý string, žiadna z nich nemôže nechtiac zmeniť obsah druhej.

To eliminuje veľké množstvo chýb.

## Hashovanie

Keďže sa obsah stringu nikdy nemení, Python môže preň vypočítať hash iba raz.

Preto možno string používať ako kľúč v dictionary alebo ako prvok množiny (`set`).

Ak by sa obsah mohol meniť, hash by prestal byť platný a slovníky by nefungovali správne.

## Efektivita

Python môže opakovane používať rovnaké stringy bez potreby vytvárať nové kópie.

Tým šetrí pamäť aj čas.

## Thread Safety

Nemenné objekty sú prirodzene bezpečnejšie pri práci vo viacerých vláknach, pretože ich obsah sa počas vykonávania programu nemení.

## Dôsledok pre programátora

Všetky metódy ako:

* `lower()`
* `upper()`
* `replace()`
* `strip()`

vracajú **nový string**.

Pôvodný text zostáva nezmenený.

To je jedna z najčastejších chýb začiatočníkov.

### Príklad

```python
text = "Python"

new_text = text.lower()
```

Po vykonaní:

* `text` stále obsahuje `"Python"`
* `new_text` obsahuje `"python"`

Pôvodný objekt sa nikdy neupravuje.
