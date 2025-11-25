# Składanie Genomu

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

- Policzy całkowitą ilość odczytów w bibliotece Illuminy
- Policzy całkowitą liczbę nukleotydów w bibliotece NanoPore
- Obliczy średnią/mediane długości odczytów w bibliotece NanoPore

Opcjonalne funkcje:

- Obliczy średnią zawartość %GC
- Wygeneruje histogram przedstawiający rozkład długości odczytów

Skrypt należy wrzucić na swojego githuba (repozytorium np. bmiw, katalog Lab_01), dodatkowo jeśli zdecydujesz się na zrobienie histogramu to również wrzuć go na github. Link do githuba prześlijw formularzu, wraz z odpowiedziami na pytania, które uzyskasz dzięki skryptowi.

## Używanie nohup

Czasami będziemy chcieli coś puścić w tle (np. składanie genomu, ponieważ trochę czasu to zajmuje a zajęcia zbliżają się ku końcowi), możemy wykorzystać dwa narzedzia `screen` oraz `nohup`, w tym przypadku `nohup` wydaje się być prostszy do wytłumaczenia i zastosowania.

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

## Kontrola jakości Illuminy i trimmowanie

> Pamietajcie by używać tyle wątków ile domyślnie podałem w poleceniu ze względu na ograniczenia obliczeniowe serwera

### FastP  

- plik_1
- plik_2
- output_1
- output_2
- filtrowanie początku i końca sekwencji
- rozmiar okna filtrowania
- srednia jakość filtrowania
- minimalna długość pozostawionych odczytów

## Kontrola jakości Nanopore

NanoPlot
  
- liczba wątków 5
- metryka N50
- plik
- output

porechop

- liczba wątków 5
- plik
- output

Filtlong

- średnia jakość
- średnia długość
- plik
- output

Nanoplot po filtracji
- liczba wątków 5
- metryka N50
- plik
- output

## Składanie genomu za pomocą SPADES i MegaHIT

> Tutaj zdecydowanie używajcie podanej liczby wątków w poleceniu, przecież nie chcemy zapchać serwera prawda?

Spades

- liczba wątków 5
- automatyczny próg coverage cutoff
- plik_1_illumina
- plik_2_illumina
- plik_nanopore
- output

MegaHit

- plik_1_illumina
- plik_2_illumina
- output
- liczba wątków 5
- m 0.5

## Porównanie wyników z Spadesa i MegaHita za pomocą Quasta

Quast

- złożenie spades
- złożenie megahit
- output

## Porównanie wyników w MultiQC

Tutaj powinniście wymienić się raportami z poszczególnych wcześniejszych kroków i (w obrębie narzędzia) porównać ze sobą wyniki, jak różnią się w obrębie badanych bakterii.
