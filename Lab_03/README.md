# Analiza filogenetyczna i identyfikacja profagów

Wersja testowa zajęć, jeśli to czytasz, to radzę poczekać na oficjalną wersję, która dostepna będzie w poniedziałek

## Instalacja niezbędnych programów

GTDB-TK
```bash
mamba create -n gtdb-tk
```
```bash
mamba activate gtdb-tk
```
```bash
mamba install bioconda::gtdbtk
```
```bash
mamba env config vars set GTDBTK_DATA_PATH="/home/jbarylski/mambaforge/envs/gtdb-tk/share/gtdbtk-2.4.0/db";
```

`GTDBTK_DATA_PATH /home/jbarylski/mambaforge/envs/gtdb-tk/share/gtdbtk-2.4.0/db`

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

## Identyfikacja profagów i Analiza filogenetyczna

GTDB-TK

```bash
gtdbtk identify --genome_dir SCIEZKA_DO_GENOMU --out_dir identyfy_out --cpus 4
```

```bash
gtdbtk align --identify_dir identyfy_out --out_dir align_out
```

```bash
gtdbtk classify --extension fasta --genome_dir SCIEZKA_DO_GENOMU --align_dir align_out --out_dir classify_out --skip_ani_screen --cpus 4
```

Anti-Smash

https://antismash.secondarymetabolites.org/#!/start

PhiSpy

Będziemy potrzebować pliku w formacie `GenBank`, znajdziesz go w folderze z plikami wyjściowymi z programu `bakta` z rozszerzeniem `.gbff`

```bash
PhiSpy.py TWÓJ_PLIK_GENBANK -o NAZWA_KATALOGU_WYJSCIOWEGO --threads 10 --color --output_choice 7
```
