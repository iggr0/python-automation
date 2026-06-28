# Chapter 5 – Dictionaries and Structuring Data

---

# 1. Dictionary Data Type

Dictionary (slovník) je jedna zo základných dátových štruktúr v Pythone. Slúži na ukladanie údajov vo forme **dvojíc kľúč – hodnota (key-value pairs)**. Každému jedinečnému kľúču je priradená presne jedna hodnota. Na rozdiel od zoznamov sa k údajom nepristupuje pomocou číselných indexov, ale pomocou názvov (kľúčov), čo robí kód prehľadnejším a jednoduchším na údržbu.

Slovníky patria medzi **mutovateľné (mutable)** dátové typy, čo znamená, že ich obsah možno po vytvorení meniť – pridávať nové položky, upravovať existujúce alebo ich odstraňovať. Samotný objekt slovníka zostáva rovnaký, mení sa iba jeho obsah.

Každý kľúč v slovníku musí byť **jedinečný**. Ak sa rovnaký kľúč použije viackrát, posledná priradená hodnota prepíše všetky predchádzajúce. Hodnoty naopak jedinečné byť nemusia a môžu sa opakovať.

Kľúč môže byť iba **hashovateľný (immutable)** objekt, napríklad:

- `str`
- `int`
- `float`
- `bool`
- `tuple` (iba ak obsahuje immutable prvky)

Naopak ako kľúč nemožno použiť:

- `list`
- `dict`
- `set`

pretože tieto objekty sú mutovateľné.

Hodnotou môže byť ľubovoľný objekt:

- číslo
- text
- boolean
- list
- tuple
- dictionary
- funkcia
- objekt triedy

Dictionary sa vytvára pomocou zložených zátvoriek `{}`.

### Príklad

```python
student = {
    "name": "Martin",
    "age": 20,
    "passed": True
}
```

---

# 2. Dictionaries vs Lists

Dictionary a List patria medzi kolekcie, avšak riešia odlišné problémy.

**List** predstavuje usporiadanú sekvenciu prvkov. Každá hodnota má svoje pevné miesto určené indexom. List je vhodný vtedy, keď je dôležité poradie údajov alebo potrebujeme pristupovať podľa pozície.

**Dictionary** predstavuje mapovanie medzi názvom (kľúčom) a hodnotou. Nepracuje s indexmi, ale s významovými identifikátormi. Vďaka tomu je vhodný na reprezentáciu objektov z reálneho sveta, databázových záznamov alebo konfigurácií.

Pri porovnávaní dvoch listov záleží na poradí prvkov. Pri dictionary je dôležité iba to, či obsahujú rovnaké dvojice kľúč–hodnota.

Dictionary nie je možné sliceovať, pretože nepracuje s indexmi.

| List | Dictionary |
|------|------------|
| Prístup cez index | Prístup cez kľúč |
| Vhodný pre sekvencie | Vhodný pre mapovanie údajov |
| Zachováva poradie prvkov | Obsahuje pomenované položky |
| Možno sliceovať | Slice nie je podporovaný |

### Príklad

```python
person = {
    "name": "Alice",
    "age": 25
}

print(person["name"])
```

---

# 3. Práca s Dictionary

So slovníkmi možno vykonávať všetky základné operácie potrebné na správu údajov.

Medzi najčastejšie operácie patrí:

- vytvorenie slovníka,
- čítanie hodnoty,
- pridanie novej položky,
- úprava existujúcej hodnoty,
- odstránenie položky.

Pri prístupe ku kľúču Python najskôr vyhľadá jeho existenciu. Ak sa kľúč nenájde a použije sa klasický prístup pomocou hranatých zátvoriek, vznikne výnimka **KeyError**.

Pridanie novej položky aj zmena existujúcej položky využívajú rovnakú syntax. Ak kľúč existuje, jeho hodnota sa prepíše. Ak neexistuje, vytvorí sa nový záznam.

Odstránenie položky sa vykonáva príkazom `del`.

### Príklad

```python
car = {
    "brand": "Toyota"
}

car["year"] = 2024
```

---

# 4. keys(), values(), items()

Dictionary poskytuje tri základné metódy na prácu s jeho obsahom.

## keys()

Vracia všetky kľúče uložené v slovníku.

Používa sa najmä v prípadoch, keď potrebujeme prechádzať jednotlivé názvy položiek alebo kontrolovať ich existenciu.

---

## values()

Vracia všetky hodnoty uložené v slovníku.

Používa sa vtedy, keď nás nezaujímajú názvy položiek, ale iba samotné údaje.

---

## items()

Vracia dvojice **(key, value)**.

Ide o najpraktickejší spôsob iterácie cez dictionary, pretože máme naraz dostupný názov položky aj jej hodnotu.

Tieto metódy nevracajú klasický zoznam, ale špeciálne pohľady (**Dictionary Views**), ktoré automaticky odrážajú zmeny vykonané v slovníku.

### Príklad

```python
for key, value in person.items():
    print(key, value)
```

---

# 5. Kontrola existencie kľúčov

Pri práci so slovníkmi je veľmi časté overovať, či určitý kľúč existuje.

Na tento účel sa používa operátor **in**.

Operátor:

```python
key in dictionary
```

nekontroluje hodnoty, ale iba kľúče.

Na kontrolu hodnôt sa používa:

```python
value in dictionary.values()
```

Kontrola existencie kľúča je veľmi efektívna a patrí medzi najväčšie výhody dictionary oproti listom.

Používa sa najmä pri:

- databázach,
- konfiguráciách,
- registráciách používateľov,
- počítaní výskytov,
- validácii vstupov.

### Príklad

```python
if "name" in person:
    print("Existuje.")
```

---

# 6. get()

Metóda **get()** umožňuje bezpečný prístup k hodnote bez rizika vzniku výnimky **KeyError**.

Ak požadovaný kľúč existuje, metóda vráti jeho hodnotu.

Ak kľúč neexistuje, vráti predvolenú hodnotu (default), ktorú určí programátor. Ak nie je zadaná, vráti hodnotu `None`.

Použitie `get()` robí program odolnejším voči chybám a eliminuje potrebu opakovane kontrolovať existenciu kľúča pomocou podmienok.

Táto metóda sa veľmi často využíva pri:

- počítaní výskytov,
- inventároch,
- štatistikách,
- spracovaní JSON dát,
- práci s API.

### Príklad

```python
inventory.get("arrow", 0)
```

---

# 7. setdefault()

Metóda **setdefault()** rozširuje funkcionalitu metódy `get()`.

Najskôr overí, či daný kľúč existuje.

- Ak existuje, vráti jeho hodnotu.
- Ak neexistuje, vytvorí nový kľúč s predvolenou hodnotou a túto hodnotu zároveň vráti.

Výhodou tejto metódy je, že jedným príkazom dokáže overiť existenciu položky aj vytvoriť nový záznam.

Najčastejšie sa používa pri:

- vytváraní počítadiel,
- zoskupovaní údajov,
- vytváraní vnorených slovníkov,
- inicializácii kolekcií.

### Príklad

```python
count.setdefault(letter, 0)
```

---

# 8. Pretty Printing (pprint)

Pri práci s veľkými alebo vnorenými dátovými štruktúrami býva klasický výpis pomocou `print()` neprehľadný.

Modul **pprint (Pretty Print)** slúži na formátovaný výpis komplexných objektov.

Jeho úlohou nie je meniť obsah údajov, ale iba ich vizuálnu prezentáciu.

Výhody:

- lepšia čitateľnosť,
- automatické odsadenie,
- prehľadnejší výpis vnorených štruktúr,
- vhodný pri ladení programov.

Modul obsahuje dve najdôležitejšie funkcie:

- `pprint()` – vypíše objekt na obrazovku,
- `pformat()` – vráti objekt ako naformátovaný text.

Pretty Printing sa často používa pri práci s JSON dátami alebo rozsiahlymi slovníkmi.

### Príklad

```python
import pprint

pprint.pprint(data)
```

---

# 9. Modelovanie reálnych dát

Jednou z hlavných myšlienok celej kapitoly je modelovanie objektov reálneho sveta pomocou dátových štruktúr.

Dictionary umožňuje prirodzene reprezentovať objekty, ktoré pozostávajú z viacerých vlastností.

Namiesto množstva samostatných premenných možno všetky údaje uložiť do jedného objektu.

Takýmto spôsobom možno reprezentovať napríklad:

- používateľa,
- študenta,
- automobil,
- produkt,
- objednávku,
- konfiguráciu programu,
- inventár hry,
- databázu narodenín.

Takýto prístup robí program:

- prehľadnejším,
- jednoduchším na údržbu,
- ľahšie rozšíriteľným.

Autor kapitoly zdôrazňuje, že neexistuje jediný správny spôsob modelovania dát. Dôležité je navrhnúť štruktúru tak, aby vyhovovala potrebám programu a bola zrozumiteľná. :contentReference[oaicite:0]{index=0}

### Príklad

```python
book = {
    "title": "Python",
    "author": "Al Sweigart",
    "pages": 504
}
```

---

# 10. Tic-Tac-Toe príklad

Autor demonštruje modelovanie reálneho objektu na hre **Piškvorky (Tic-Tac-Toe)**.

Hracia plocha pozostáva z deviatich polí.

Každé pole predstavuje jeden kľúč dictionary.

Takýto návrh je omnoho čitateľnejší ako použitie číselných indexov, pretože názov kľúča okamžite určuje pozíciu na hracej ploche.

Výhody tohto prístupu:

- jednoduché vyhľadávanie polí,
- ľahká modifikácia,
- intuitívny zápis,
- dobrá čitateľnosť programu.

Tento príklad ukazuje, že dátové štruktúry môžu predstavovať abstraktný model reálneho objektu.

### Príklad

```python
board["top-L"] = "X"
```

---

# 11. Vnorené slovníky a zoznamy

Veľké aplikácie spravidla nepracujú iba s jedným dictionary.

Jednotlivé dátové štruktúry sa navzájom kombinujú.

Najčastejšie kombinácie sú:

- List obsahuje dictionaries.
- Dictionary obsahuje list.
- Dictionary obsahuje ďalší dictionary.

Takéto dátové štruktúry označujeme ako **vnorené (nested)**.

Vnorené štruktúry umožňujú reprezentovať veľmi komplexné objekty bez potreby vytvárať množstvo samostatných premenných.

Používajú sa napríklad pri:

- JSON súboroch,
- webových API,
- databázach,
- konfiguráciách,
- hrách,
- informačných systémoch.

Pri práci s vnorenými štruktúrami je potrebné postupovať po jednotlivých úrovniach.

### Príklad

```python
company["employees"]["manager"]
```

---

# 12. Zhrnutie

Dictionary patrí medzi najvýznamnejšie dátové štruktúry Pythonu.

Jeho hlavnou výhodou je rýchle vyhľadávanie údajov pomocou pomenovaných kľúčov.

Najdôležitejšie vlastnosti:

- ukladá dvojice key–value,
- kľúče musia byť jedinečné,
- hodnoty sa môžu opakovať,
- patrí medzi mutable objekty,
- umožňuje efektívne vyhľadávanie,
- výborne modeluje objekty reálneho sveta,
- podporuje vnorené dátové štruktúry,
- obsahuje množstvo vstavaných metód na prácu s údajmi.

Dictionary je jednou z najčastejšie používaných dátových štruktúr nielen v Pythone, ale aj vo väčšine moderných programovacích jazykov.

---

# 13. Big-O zložitosť

Dictionary je implementovaný pomocou **hash tabuľky (Hash Table)**.

Hash tabuľka využíva hash funkciu, ktorá prevádza kľúč na internú adresu v pamäti. Vďaka tomu nie je potrebné prehľadávať celý slovník pri každom vyhľadávaní.

Priemerná časová zložitosť najčastejších operácií je:

| Operácia | Zložitosť |
|----------|-----------|
| Vyhľadanie podľa kľúča | O(1) |
| Pridanie položky | O(1) |
| Aktualizácia položky | O(1) |
| Odstránenie položky | O(1) |
| Kontrola `key in dict` | O(1) |
| Iterácia cez celý dictionary | O(n) |
| Vyhľadávanie hodnoty | O(n) |

Dictionary je preto výrazne efektívnejší ako list pri vyhľadávaní podľa identifikátora.

---

# 14. Najčastejšie chyby

Najčastejšie chyby pri práci s dictionaries: 

- prístup k neexistujúcemu kľúču (`KeyError`),
- zámena kľúčov a hodnôt,
- používanie mutovateľných objektov ako kľúčov,
- predpokladanie existencie poradia položiek,
- zmena dictionary počas iterácie,
- zbytočné nepoužívanie metódy `get()`,
- vytváranie príliš hlboko vnorených dátových štruktúr,
- používanie nejasných názvov kľúčov.

Dodržiavanie správnych návrhových princípov a používanie vstavaných metód (`get()`, `setdefault()`, `items()`) vedie k čitateľnejšiemu, bezpečnejšiemu a efektívnejšiemu programu.

### Príklad

```python
user.get("email", "Nezadaný email")
```
# Význam dictionary pri JSON a AI

## Dictionary a JSON

JSON znamená **JavaScript Object Notation** a používa sa na výmenu dát medzi programami, servermi, webovými aplikáciami, API službami a databázami.

JSON objekt vyzerá veľmi podobne ako Python dictionary:

```json
{
  "name": "Alice",
  "age": 25,
  "city": "Bratislava"
}
```

V Pythone by rovnaké dáta vyzerali takto:

```python
{
    "name": "Alice",
    "age": 25,
    "city": "Bratislava"
}
```

Hlavný význam je v tom, že keď program komunikuje s webovou službou alebo API, dáta často prichádzajú práve vo forme JSON. Python ich potom vie jednoducho previesť na dictionary a ďalej s nimi pracovať.

Napríklad API môže vrátiť údaje o používateľovi, počasí, produkte alebo objednávke. Program tieto údaje načíta ako dictionary a môže pristupovať ku konkrétnym hodnotám pomocou kľúčov.

Preto je dictionary základom práce s:

- API,
- webovými aplikáciami,
- databázami,
- konfiguračnými súbormi,
- dátami zo servera,
- JSON odpoveďami,
- automatizáciou.

---

## Dictionary a AI

V AI sa dictionary používa najmä na reprezentáciu vlastností objektov, vstupných dát, výsledkov modelov a konfigurácií.

Napríklad jeden vstup pre AI model môže vyzerať takto:

```python
{
    "text": "Tento produkt je výborný.",
    "language": "sk",
    "task": "sentiment_analysis"
}
```

Takýto dictionary hovorí modelu:

- aký text má spracovať,
- v akom jazyku je text,
- akú úlohu má vykonať.

AI model môže vrátiť výsledok tiež ako dictionary:

```python
{
    "sentiment": "positive",
    "confidence": 0.94
}
```

To znamená, že model vyhodnotil text ako pozitívny a je si tým istý na 94 %.

Dictionary sa v AI používa napríklad pri:

- spracovaní vstupov pre model,
- ukladaní výsledkov predikcie,
- reprezentácii parametrov modelu,
- práci s datasetmi,
- spracovaní odpovedí z AI API,
- ukladaní metadát,
- konfigurácii tréningu modelov.

V oblasti generatívnej AI sa dictionary často používa aj na tvorbu správ pre model.

Napríklad správa pre chatovací model môže mať podobu:

```python
{
    "role": "user",
    "content": "Vysvetli mi dictionaries v Pythone."
}
```

Tu kľúč `"role"` určuje, kto správu posiela, a kľúč `"content"` obsahuje samotný text správy.

---

## Prečo je to dôležité

Dictionary je dôležitý preto, že umožňuje ukladať dáta tak, aby mali význam.

Namiesto anonymných hodnôt v zozname:

```python
["Alice", 25, "Bratislava"]
```

máme pomenované údaje:

```python
{
    "name": "Alice",
    "age": 25,
    "city": "Bratislava"
}
```

Druhá verzia je jasnejšia, čitateľnejšia a vhodnejšia pre komunikáciu medzi systémami.

V JSON aj AI platí, že nestačí mať iba hodnoty. Dôležité je vedieť, čo tieto hodnoty znamenajú. Práve to zabezpečujú kľúče v dictionary.

Preto možno povedať:

> Dictionary je základný spôsob, ako v Pythone reprezentovať štruktúrované dáta.

A práve štruktúrované dáta sú základom webových aplikácií, API, JSON komunikácie aj umelej inteligencie.