# JEŚLI TO CZYTASZ TO ZNACZY ŻE JEST TO NIEAKTUALNE, POCZEKAJ NA ODPOWIEDNIE ZAJĘCIA :D

## Analiza taksonomiczna, identyfikacja profagów, bioprospecting

Zidentyfikuj do jakich taksonów(gantunku/rodzaju/rodziny) należy analizowana przez Ciebie bakteria, zidentyfikuj występujące w niej profagi.

## Instalacja niezbędnych programów

### GTDB-TK
```bash
mamba create -n gtdb-tk
```
```bash
mamba activate gtdb-tk
```
```bash
mamba install bioconda::gtdbtk
```
Baza danych sciągała się kilka godzin dlatego skorzystamy z tej pobranej

UWAGA! TEJ KOMENDY NIE WYKONUJEMY 
```bash
$ download-db.sh #NIE URUCHAMIAĆ!
```
Ustawianie ścieżki do pobranej wcześniej bazy danych

```bash
mamba env config vars set GTDBTK_DATA_PATH="/home/database/miniforge3/envs/gtdb-tk/share/gtdbtk-2.5.2/db/;
```

Teraz musimy zrestartować środowisko
```bash
mamba deactivate
```
```bash
mamba activate gtdb-tk
```

I możemy przejść do instalacji kolejnego programu :)

### PhiSpy

```bash
mamba create -n phispy
```
```bash
mamba activate phispy
```
```bash
mamba install -c bioconda phispy
```

## Analiza taksonomiczna, identyfikacja profagów, bioprospecting

### GTDB-TK

```bash
mkdir genomes/
```

```bash
cp ŚCIEŻKA_DO_TWOJEGO_GENOMU_ZE_SPADESA genomes/
```

```bash
gtdbtk identify --genome_dir genomes/  --out_dir identyfy_out --extension fasta  --cpus 3
```

```bash
gtdbtk align --identify_dir identyfy_out --out_dir align_out
```

```bash
gtdbtk classify --extension fasta --genome_dir genomes/ --align_dir align_out --out_dir classify_out --skip_ani_screen --cpus 3
```

### PhiSpy

Będziemy potrzebować pliku w formacie `GenBank`, znajdziesz go w folderze z plikami wyjściowymi z programu `bakta` z rozszerzeniem `.gbff`

```bash
PhiSpy.py TWÓJ_PLIK_GENBANK -o NAZWA_KATALOGU_WYJSCIOWEGO --threads 3 --output_choice 7
```


