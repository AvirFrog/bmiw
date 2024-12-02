# Składanie Genomu

Przeanalizuj i złóż [bibliotek z sekwencjonowania genomu Agreia sp. (bakteria)](https://www.ebi.ac.uk/ena/browser/view/PRJEB40363)

##  Instalacja Condy i Mamby

Pobieranie miniforge

```bash
wget https://github.com/conda-forge/miniforge/releases/download/24.9.2-0/Mambaforge-24.9.2-0-Linux-x86_64.sh
```

```bash
chmod +x Mambaforge-24.9.2-0-Linux-x86_64.sh
```

```bash
./Mambaforge-24.9.2-0-Linux-x86_64.sh
```

```bash
conda config --add channels bioconda
```
## Tworzenie wirtualnych środowisk

--> `Dobrą praktyką (i bezpieczną) jest tworzenie osobnego środowiska do każdego narzędzia, ale jest to wymagane tylko dla niektórych programów.` <--

Tworzenie witrualnego środowiska
```bash
mamba create -n env_name
```

Aktywowanie utworzonego wirtualnego środowiska
```bash
mamba activate NAZWA_SRODOWISKA
```

Sprawdzenie jakie środowiska są już utworzone
```bash
mamba env list
```

## Instalacja niezbędnych programów

FastQC (narzędzie do kontroli jakości odczytów Illumina)
```bash
mamba install bioconda::fastqc
```

FastP (narzędzie do kontroli jakości, filtrowania i przycinania odczytów Illumina)
```bash
mamba install bioconda::fastp
```

NanoPlot (narzędzie do kontroli jakości odczytów NanoPore)
```bash
mamba install bioconda::nanoplot
```

Porechop (narzędzie do usuwania adaptorów z NanoPore)
```bash
mamba install bioconda::porechop
```

Filtlong (narzędzie do filtrowania odczytów NanoPore)
```bash
mamba install bioconda::filtlong
```

spades (uniwersalny program do składania odzytów Illumina i bibliotek mieszanych - np. Illimina i Nanopore)
```bash
mamba install bioconda::spades
```

MegaHit (program do składania odzytów Illumina)
```bash
mamba install bioconda::megahit
```

Quast (narzędzie do kontroli jakości złożenia)
```bash
mamba install bioconda::quast
```


--> `Quasta najlepiej dodac do nowego środowiska` <--

## Pobieranie danych

[biblioteka z sekwencjonowania genomu Agreia sp. (bakteria)](https://www.ebi.ac.uk/ena/browser/view/PRJEB40363)

Prościej może być jak ręczne pobierzemy danych i przerzucimy je na serwer za pomocą WinSCP

lub jeśli ktoś chce używać SCP w linuxie to przyda się ta komenda:

```bash
scp *.fastq.gz {myuser}@IP_SERWERA_PODANE_NA_TEAMS:/path/to/dir
```

## Kontrola jakości Illuminy i trimmowanie

FastP  
```bash
fastp -i PLIK_DO_ANALIZY_1.fastq.gz -I PLIK_DO_ANALIZY_2.fastq.gz -o output_1_trimmed.fastq.gz -O output_2_trimmed.fastq.gz --cut_front --cut_tail --cut_window_size 4 --cut_mean_quality 30 --length_required 50
```

## Kontrola jakości Nanopore

NanoPlot
  
```bash
NanoPlot -t 5 --N50 --fastq PLIK_DO_ANALIZY.fastq.gz -o prefilter_nanoplot
```

porechop
```bash
porechop -t 5 -i PLIK_DO_ANALIZY.fastq.gz -o prefiltered_nanopore.fastq
```

Fitlong
```bash
filtlong --min_mean_q 90 --min_length 1000 prefiltered_nanopore.fastq > filtered_nanopore.fastq
```

Nanoplot po filtracji
```bash
NanoPlot -t 5 --N50 --fastq filtered_nanopore.fastq -o postfilter_nanoplot
```

## Używanie nohup

Czasami zdazy się taka sytacja że będziemy chcieli coś puścić w tle (np. składanie genomu, ponieważ trochę czasu to zajmuje a zajęcia zbliżają się ku końcowi), możemy wykorzystać dwa narzedzia `screen` oraz `nohup`, w tym przypadku `nohup` wydaje się być prostszy do wytłumaczenia i zastosowania.

Poniżej jak wyglada przykładowa komenda `nohup`

```bash
nohup [nasza_komenda] > output.log 2> &1 &
```

- `nohup` - komenda za pomocą, której uruchomimy coś w tle
- `[nasza_komenda]` - tu wklejamy nasze polecenie, które chcemy wykonać
- `> output.log` - możemy nazwać output jak chcemy, jest  to przekierowanie informacji z standard outputu do pliku
- `2> &1` - jest to przekierowania standard error do pliku który podalismy wcześniej (alternatywnie możemy zrobić tak `> stdr_out.txt 2> stdr_err.txt` i wtedy standard output i error mamy w osobnych plikach)
- `&` - końcowy ampersant jest niezbędny do uruchomienia polecenia nohup

## Składanie genomu za pomocą SPADES i MegaHIT

Spades
```bash
spades.py -t 5 --cov-cutoff auto --pe1-1 PLIK_DO_ANALIZY_illumina_trimmed_1.fastq.gz --pe1-2 PLIK_DO_ANALIZY_illumina_trimmed_2.fastq.gz --nanopore PLIK_DO_ANALIZY_filtered_nanopore.fastq -o spades_assembly
```

MegaHit
```bash
megahit -1 PLIK_DO_ANALIZY_illumina_trimmed_1.fastq.gz -2 PLIK_DO_ANALIZY_illumina_trimmed_2.fastq.gz -o megahit_output -t 5 -m 0.5
```

## Porównanie wyników z Spadesa i MegaHita za pomocą Quasta

Quast
```bash
quast ./spades_assembly/scaffolds.fasta ./megahit_output/final.contigs.fa -o quast_comparision
```
