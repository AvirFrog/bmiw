# Składanie Genomu

Jeśli z jakiegoś powodu w twoim katalogu domowym nie ma katalogu `dane` to pobierz je ręcznie (to którą bakterie bedziesz analizować dowiesz się na zajęciach)

[1. Agreia sp.](https://www.ebi.ac.uk/ena/browser/view/PRJEB40363)

[2. XXX](www.google.pl)

[3. XXX](www.google.pl)

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

Teraz należy się przelogować

```bash
conda config --add channels bioconda
```
## Tworzenie wirtualnych środowisk

> Dobrą praktyką (i bezpieczną) jest tworzenie osobnego środowiska do każdego narzędzia, ale jest to wymagane tylko dla niektórych programów.

Tworzenie witrualnego środowiska
```bash
mamba create -n NAZWA_SRODOWISKA
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

Do instalacji programów przyda się poniższa komenda gdzie `NAZWA_PROGRAMU` powinna zostać zastąpiona nazwą instalowanego programu. Polecam sprawdzić jak dokładnie sie program nazywa (czasem podczas instalacji podajemy delikatnie inną nazwę niż tą, którą program posiada) wpisując w przeglądarkę "`NAZWA_PROGRAMU` conda installation". 

My zamiast `condy` użyjemy `mamby` bo jest szybsza i lepsza. 

```bash
mamba install bioconda::NAZWA_PROGRAMU
```

### Lista programów do zainstalowania

> Jeśli zainstalujecie wszystkie na początku będzie prościej w dalszej cześci zajęć ;)

- FastP (narzędzie do kontroli jakości, filtrowania i przycinania odczytów Illumina)
- NanoPlot (narzędzie do kontroli jakości odczytów NanoPore)
- Porechop (narzędzie do usuwania adaptorów z NanoPore)
- Filtlong (narzędzie do filtrowania odczytów NanoPore)
- Spades (uniwersalny program do składania odzytów Illumina i bibliotek mieszanych - np. Illimina i Nanopore)
- MegaHit (program do składania odzytów Illumina)
- Quast (narzędzie do kontroli jakości złożenia)
- MultiQC (narzedzie do łączenia kilku raportów w jeden)

> Quasta najlepiej dodac do nowego środowiska

## Zadanie 1

Napisz skrypt w pythonie, który:

- Policzy całkowitą ilość odczytów w próbkach 
- Policzy całkowitą liczbę nukleotydów w próbkach
- Obliczy średnią/mediane długości odczytów w próbkach
- Poda najkrótszy i najdłuższy odczyt

Opcjonalne funkcje:

- Obliczy średnią zawartość %GC
- Wygeneruje histogram przedstawiający rozkład długości odczytów

Skrypt należy wrzucić na swojego githuba (repozytorium np. bmiw, katalog Lab_01), dodatkowo jeśli zdecydujesz się na zrobienie histogramu to również wrzuć go na github. Link do githuba prześlijw formularzu, wraz z odpowiedziami na pytania, które uzyskasz dzięki skryptowi.

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

Filtlong
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

żeby sprawdzić czy nasz skrypt działa uzywamy komendy
```bash
jobs
```
Jeśli mamy `Running` to znaczy że nasze zadanie dalej jest w trakcie pracy, jeśli mamy `Done` znaczy ze zadanie sie wykonało a jeśli jest `Exit` lub `Terminated` to znaczy że coś poszło nie tak i należy sprawdzić nasz plik z outputem/z standard errorem


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
