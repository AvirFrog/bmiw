# Adnotacja genomu bakterii

Przeporwadź adnotację genomu dwoma metodami oraz porównanaj wyniki i wyszukaj geny o konkretnych funkcjach za pomocą własnego skryptu w **Pythonie**

## Instalacja niezbędnych programów

W razie problemów z programami Prokka lub Bakta można skorzystać z serwerów galaxy, na których znajdują się te narzędzia: https://usegalaxy.eu / https://usegalaxy.org / https://usegalaxy.org.au

Prokka (nieco starszy leczpowszechnie używany zestaw do adnotacji pozycji i funkcji genów)

```bash
mamba create -n prokka_blast
```
```bash
mamba activate prokka_blast
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
mamba install bioconda::bakta
```
Zamiast pobierać kilkudziesięcio gigabajtową bazę danych można skorzystać z tej pobranej już na serwerze, która znajduje się w `jbarylski/data_bases`, lub pobrać wersję `light` (oczywiście nie będzie tak dobra jak pełna wersja bazy ale do ćwiczeń wystarczy) za pomocą poniższych komend:

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

Poniższa komenda jest poglądowa, nie uruchamiajcie jej na serwerze z dwóch powodów, pobieranie zajmię za duzo czasu, rozpakowana baza danych to ponad 70GB co spowoduje niepotrzebne zapchanie serwera
```bash
bakta_db download --output bakta_db --type full
```

--> `Bakta: jeżeli wykonujesz analizę na Galaxy w "Selection of the output files" trzeba zaznaczyć "Annotations and sequences in GenBank format"` <--


## Adnotacja funkcjonalna sekwencji

Prokka (nieco starszy leczpowszechnie używany zestaw do adnotacji pozycji i funkcji genów)
```bash
prokka --outdir prokka_output --prefix assembly --genus YourGenusName --kingdom Bacteria assembly.fna --addgenes
```
lub https://usegalaxy.eu / https://usegalaxy.org / https://usegalaxy.org.au

Bakta (nowoczesny zestaw do wystandaryzowanej adnotacji pozycji i funkcji genów u bakterii)
```bash
bakta --db <db-path> --verbose --output results_bakta/ --prefix assembly --threads 3 WASZ_GENOM.fasta
```

lub https://usegalaxy.eu / https://usegalaxy.org / https://usegalaxy.org.au

## Porównanie wyników adnotacji uzyskanych różnymi metodami

[BEACON](https://www.cbrc.kaust.edu.sa/BEACON) (webserver do porównywania adnotacji W FORMACIE GENBANK)


## Analiza wybranych rodzin genowych

Samodzielnie napisz skrypt, który wyodrębni z genomu geny kodujące polimerazy RNA i DNA (np korzystając z biblioteki SeqIO pakietu biopython).
