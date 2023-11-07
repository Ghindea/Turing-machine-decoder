# Mașină Turing pentru decodificarea codului Morse și identificarea unor cuvinte cheie

Temă realizată în cadrul cursului de Analiza Algoritmilor, anul II, ACS-CTI

made by: *Daniel Ghindea*, *325CB*

---
Tabela de tranziții a mașinii Turing se găsește în fișierul morse.xlsx. Pentru a o converti în cod mașină și a o rula în [simulatorul Turing](https://turingmachinesimulator.com/) se va folosi comanda:
```
python checker.py  --tm morse.xlsx  --output translate.tms
```
Pentru rularea checkerului se va folosi comanda
```py
python3 checker.py --tm morse.xlsx --run-tests
```

Mașina Turing parcurge banda care inițial conține doar caractere din mulțimea {" . ", " - ", " * ", " / ", " _ "}. Identificarea literelor pe baza acestor caractere se realizează utilizând următoarea schemă.

```

    E --------> A --------> W --------> J   .---
    |           |           |
    |           |           + --------> P   .--.
    |           |
    |           + --------> R --------> □   .-.-
    |                       |
    |                       + --------> L   .-..
    |
    + --------> I --------> U --------> □   ..--
                |           |
                |           + --------> F   ..-.
                |
                + --------> S --------> V   ...-
                            |
                            + --------> H   ....

    T --------> M --------> O --------> □   ----
    |           |           |
    |           |           + --------> □   ---.
    |           |
    |           + --------> G --------> Q   --.-
    |                       |
    |                       + --------> Z   --..
    |
    + --------> N --------> K --------> Y   -.--
                |           |
                |           + --------> C   -.-.
                |
                + --------> D --------> X   -..-
                            |
                            + --------> B   -...
(vezi legenda)
```

**Procesul de decodificare** constă în următorii pași:

* Identificarea caracterului de pe poziția curentă (starea inițială q0);
* Inlocuirea caracterului curent cu _ (ștergerea de pe bandă);
* Trecerea la starea următoare aferentă (pentru . sau - se va trece într-o stare corespunzătoare de identificare a literei; pentru * se va parcurge banda până la final (primul _ găsit) și se va scrie litera corespunzătoare; pentru / se va parcurge banda și se va plasa caracterul /);
* Dacă în stadiul anterior a fost printată o literă sau /, banda este parcursă de la capăt la început (primul _ găsit) și se reia procesul (întoarcere în q0) până au fost eliminate toate caracterele din mulțimea inițială.

**Procesul de identificare** a cuvintelor cheie începe după ce s-a finalizat decodificarea mesajului și constă în parcurgerea benzii, iar în cazul întâlnirii literelor S sau H se verifică dacă după acestea urmează O și S, respectiv E, L și P. Banda e parcursă până la final, iar în cazul în care au fost găsite cuvintele cheie se oprește în starea Y (yes), altfel în starea N (no).

---

**Legendă**:

```
--------> caracterul anterior urmat de linie
```

```
|
+-------> caracterul anterior urmat de punct
```
