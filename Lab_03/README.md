# Analiza filogenetyczna i identyfikacja profagów

Wersja testowa zajęć, jeśli to czytasz, to radzę poczekać na oficjalną wersję, która dostepna będzie w poniedziałek

## Instalacja niezbędnych programów

GTDB-TK

XXX

PhiSpy

```bash
mamba create -n phispy
```
```bash
mamba activate phispy
```
```bash
mamba install -c bioconda phispy
```
Phigaro

XXX

## Identyfikacja profagów

GTDB-TK

XXX

PhiSpy

Będziemy potrzebować pliku w formacie `GenBank`, znajdziesz go w folderze z plikami wyjściowymi z programu `bakta` z rozszerzeniem `.gbff`

```bash
PhiSpy.py TWÓJ_PLIK_GENBANK -o NAZWA_KATALOGU_WYJSCIOWEGO --threads 10 --color --output_choice 512
```

Phigaro

XXX
