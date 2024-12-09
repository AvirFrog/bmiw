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
Baza danych sciągała się ponad 2 dni dlatego skorzystamy z tej pobranej

UWAGA! TEJ KOMENDY NIE WYKONUJEMY 
```bash
$ download-db.sh #NIE URUCHAMIAĆ!
```
Ustawianie ścieżki do pobranej wcześniej bazy danych

```bash
mamba env config vars set GTDBTK_DATA_PATH="/home/jbarylski/mambaforge/envs/gtdb-tk/share/gtdbtk-2.4.0/db";
```

`GTDBTK_DATA_PATH /home/jbarylski/mambaforge/envs/gtdb-tk/share/gtdbtk-2.4.0/db`

Teraz musimy zrestartować środowisko
```bash
mamba deactivate
```
```bash
mamba activate gtdb-tk
```

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
mkdir genomes/
```

```bash
cp GENOM_ZESPADESA genomes/
```

```bash
gtdbtk identify --genome_dir genomes/  --out_dir identyfy_out --extension fasta  --cpus 3
```

```bash
gtdbtk align --identify_dir identyfy_out --out_dir align_out
```

```bash
gtdbtk classify --extension fasta --genome_dir SCIEZKA_DO_GENOMU --align_dir align_out --out_dir classify_out --skip_ani_screen --cpus 3
```

Anti-Smash

https://antismash.secondarymetabolites.org/#!/start

PhiSpy

Będziemy potrzebować pliku w formacie `GenBank`, znajdziesz go w folderze z plikami wyjściowymi z programu `bakta` z rozszerzeniem `.gbff`

```bash
PhiSpy.py TWÓJ_PLIK_GENBANK -o NAZWA_KATALOGU_WYJSCIOWEGO --threads 3 --color --output_choice 7
```
