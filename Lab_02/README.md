# JEŚLI TO CZYTASZ TO ZNACZY ŻE JEST TO NIEAKTUALNE, POCZEKAJ NA ODPOWIEDNIE ZAJĘCIA :D


## Adnotacja genomu bakterii

*https://www.ncbi.nlm.nih.gov/refseq/annotation_prok*

*https://www.microbiologyresearch.org/content/journal/mgen/10.1099/mgen.0.000927*

Przeporwadź adnotację genomu dwoma metodami oraz porównanaj wyniki i wyszukaj geny o konkretnych funkcjach za pomocą własnego skryptu w **Pythonie**

## Instalacja niezbędnych programów

W razie problemów z programami Prokka lub Bakta można skorzystać z serwerów galaxy, na których znajdują się te narzędzia: https://usegalaxy.org / https://annotation.usegalaxy.eu

Prokka (nieco starszy leczpowszechnie używany zestaw do adnotacji pozycji i funkcji genów)

```bash
mamba create -n prokka
```
```bash
mamba activate prokka
```
```bash
mamba install bioconda::blast=2.2.31
```
```bash
mamba install bioconda::prokka
```
```bash
prokka --setupdb
```

Bakta (nowoczesny zestaw do wystandaryzowanej adnotacji pozycji i funkcji genów u bakterii)
```bash
mamba create -n bakta
```

```bakta
mamba activate bakta
```

```bash
mamba install bioconda::bakta
```

Zamiast pobierać kilkudziesięcio gigabajtową bazę danych można skorzystać z wersji `light` (oczywiście nie będzie tak dobra jak pełna wersja bazy ale do ćwiczeń wystarczy) za pomocą poniższych komend:

```bash
mkdir bakta_db 
```
```bash
cd bakta_db
```
```bash
wget https://zenodo.org/record/10522951/files/db-light.tar.gz
```
```bash
tar -xzf db-light.tar.gz
```
```bash
rm db-light.tar.gz
```
```bash
cd ..
```

Poniższa komenda jest poglądowa, nie uruchamiajcie jej na serwerze z dwóch powodów, pobieranie zajmię za duzo czasu, rozpakowana baza danych to ponad 70GB co spowoduje niepotrzebne zapchanie serwera
```bash
$ bakta_db download --output bakta_db --type full #tego nie puszczać na serwerze
```

--> `Bakta: jeżeli wykonujesz analizę na Galaxy w "Selection of the output files" trzeba zaznaczyć "Annotations and sequences in GenBank format"` <--


## Adnotacja funkcjonalna sekwencji

Prokka (nieco starszy leczpowszechnie używany zestaw do adnotacji pozycji i funkcji genów)
```bash
prokka --outdir prokka_output --prefix assembly --genus NAZWA_BAKTERII --kingdom Bacteria PLIK_FASTA_ZE_ZŁOZENIA --addgenes
```
lub https://usegalaxy.org / https://annotation.usegalaxy.eu 

Bakta (nowoczesny zestaw do wystandaryzowanej adnotacji pozycji i funkcji genów u bakterii)
```bash
amrfinder_update --force_update --database bakta_db/db-light/amrfinderplus-db/
```
```bash
bakta --db bakta_db/db-light --verbose --output results_bakta/ --prefix assembly --threads 3 WASZ_GENOM.fasta
```

lub https://usegalaxy.org / https://annotation.usegalaxy.eu 
`Konieczne jest wybranie genomu, i wersji bazy AMRFinderPlus`

## Porównanie wyników adnotacji uzyskanych różnymi metodami i analiza wybranych rodzin genowych

*dodać szczegółową instrukcję pisania skryptu*

Samodzielnie napisz skrypt, który porównuje ilość i średnią długość genów w obu adnotacjach i wyodrębni z genomu geny kodujące polimerazy RNA i DNA (np korzystając z biblioteki SeqIO pakietu biopython).
Porównujemy pliki `.gbff` z `bakta` i `.gbk` z `prokka`.
