# Adnotacja genomu bakterii

Przeporwadzeniu adnotacji genomu dwoma metodami oraz porównanie wyników i wyszukanie genów o konkretnych funkcjach za pomocą własnego skryptu w **Pythonie**

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

Warto się zastanowić nad pobieraniem całej bazy danych, można też przekopiować ją z serwera z folderu `jbarylski/data_bases`
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
bakta annotate --outdir bakta_output --prefix assembly assembly.fna
```
lub https://usegalaxy.eu / https://usegalaxy.org / https://usegalaxy.org.au

## Porównanie wyników adnotacji uzyskanych różnymi metodami

[BEACON](https://www.cbrc.kaust.edu.sa/BEACON) (webserver do porównywania adnotacji W FORMACIE GENBANK)


## Analiza wybranych rodzin genowych

Samodzielnie napisz skrypt, który wyodrębni z genomu geny kodujące polimerazy RNA i DNA (np korzystając z biblioteki SeqIO pakietu biopython).
