# Adnotacja genomu bakterii

Przeprowadź adnotację genomu narzędziem Bakta

## Instalacja niezbędnych programów

W razie problemów z programem Bakta można skorzystać z serwerów galaxy, na których znajdują się te narzędzia: https://usegalaxy.org / https://annotation.usegalaxy.eu

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
bakta_db download --output bakta_db --type light
```

Poniższa komenda jest poglądowa, nie uruchamiajcie jej na serwerze z dwóch powodów, pobieranie zajmię za duzo czasu, rozpakowana baza danych to ponad 70GB co spowoduje niepotrzebne zapchanie serwera
```bash
$ bakta_db download --output bakta_db --type full #tego nie puszczać na serwerze
```

--> `Bakta: jeżeli wykonujesz analizę na Galaxy w "Selection of the output files" trzeba zaznaczyć "Annotations and sequences in GenBank format"` <--

Adnotacje z pełnej bazy danych znajdziecie w katalogu użytkownika `database`

## Adnotacja funkcjonalna sekwencji

```bash
bakta --db bakta_db/db-light --verbose --output results_bakta/ --prefix assembly --threads 3 WASZ_GENOM.fasta
```

lub https://usegalaxy.org / https://annotation.usegalaxy.eu 
`Konieczne jest wybranie genomu, i wersji bazy AMRFinderPlus`

## Zadanie 2

Napisz skrypt w pythonie, który porówna wyniki z bazy danych w wersji `light` i `full`(szczegóły znajdziecie w raporcie).
