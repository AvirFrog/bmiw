# Analiza filogenetyczna i identyfikacja profagów

Wersja testowa zajęć, jeśli to czytasz, to radzę poczekać na oficjalną wersję, która dostepna będzie w poniedziałek

## Instalacja niezbędnych programów

GTDB-TK

```bash
gtdbtk identify --genome_dir genomes --out_dir indentify_out --cpus 4
```

```bash
gtdbtk align --identify_dir indentify_out --out_dir align_out
```

```bash
gtdbtk classify --extension fasta --genome_dir genomes --align_dir align_out --out_dir classify_out --
```

```bash
skip_ani_screen --cpus 10
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

## Identyfikacja profagów

GTDB-TK

XXX

PhiSpy

Będziemy potrzebować pliku w formacie `GenBank`, znajdziesz go w folderze z plikami wyjściowymi z programu `bakta` z rozszerzeniem `.gbff`

```bash
PhiSpy.py TWÓJ_PLIK_GENBANK -o NAZWA_KATALOGU_WYJSCIOWEGO --threads 10 --color --output_choice 7
```
