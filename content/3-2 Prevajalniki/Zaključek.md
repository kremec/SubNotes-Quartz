Vhod:
- podatkovni deli: statične spremenljivke in konstante
- programerski deli: seznam funkcij, vsaka opisana s klicnim zapisom in strojnimi ukazi jedra

Izhod: zbirnik

Prevod funkcije v zbirnik: manjkata prolog in epilog, odvisna od arhitekture in klicnega dogovora

Prolog:
- shranimo registre
- ustvarimo klicni zapis
- skočimo na LABEL entry

Epilog:
- restavriramo registre
- podremo klicni zapis
- pripravimo rezultat
- izvršimo "RETURN"

Inicializacijska koda, ki se požene še pred main:
- pripravi sklad, kopico, statične spremenljivke
- klic funkcije main
- rezultat vrnemo v OS
- signal OS za ukinitev procesa

Dodan kos zbirnika z definicijami funkcijskih prototipov:
- `malloc`, `free`
- `putc`, `putint`, ..., `getc`, ...