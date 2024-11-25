# Składanie Genomu

##  Instalacja Condy i Mamby
<details>

<summary>Pobieranie miniforge</summary>

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
  
</details>


## Instalacja niezbędnych programów

Dobrą praktyką (i bezpieczną) jest tworzenie osobnego środowiska do każdego narzędzia, ale nie jest to wymagane.

<details>
<summary> Tworzenie nowego środowiska </summary>

```bash
mamba create -n env_name
```
</details>

Instalacja potrzebnych narzędzi:

<details>
<summary>FastQC</summary>
  
```bash
mamba install bioconda::fastqc
```
</details>

<details>
<summary>FastP</summary>
  
```bash
mamba install bioconda::fastp
```
</details>

<details>
<summary>spades</summary>
  
```bash
mamba install bioconda::spades
```
</details>

<details>
<summary>MegaHit</summary>
  
```bash
mamba install bioconda::megahit
```
</details>

<details>
<summary>Quast</summary>
  
```bash
mamba install bioconda::quast
```
</details>

<details>
<summary>MultiQC</summary>
  
```bash
mamba install bioconda::multiqc
```
</details>

## Pobieranie danych

Będziemy potrzebować jeszcze jednego narzędzia:

<details>
<summary>SRA tools</summary>
  
```bash
mamba install bioconda::sra-tools
```
</details>

Pobieramy dane: 

<details>
<summary>Jak pobrać dane?</summary>
  
```bash
fastq-dump --gzip --skip-technical --readids --read-filter pass --dumpbase --split-3 --clip --outdir path/to/output/ ID_PROJEKTU
```
</details>

```txt
Prościej może być jak ręczne pobierzemy danych i przerzucenie ich na serwer za pomocą WinSCP
```
## Kontrola jakości Illuminy

<details>
<summary>FastP</summary>
  
```bash
fastp -i PLIK_DO_ANALIZY_1.fastq.gz -I PLIK_DO_ANALIZY_2.fastq.gz -o output_1_trimmed.fastq.gz -O output_2_trimmed.fastq.gz --cut_front --cut_tail --cut_window_size 4 --cut_mean_quality 30 --length_required 50
```
</details>



## Kontrola jakości Nanopore

<details>
<summary>NanoPlot</summary>
  
```bash
NanoPlot -t 5 --N50 --fastq PLIK_DO_ANALIZY.fastq.gz -o prefilter_nanoplot
```
</details>

<details>
<summary>porechop</summary>
  
```bash
porechop -t 5 -i PLIK_DO_ANALIZY.fastq.gz -o prefiltered_nanopore.fastq
```
</details>

<details>
<summary>Fitlong</summary>
  
```bash
filtlong --min_mean_q 95 --min_length 1000 prefiltered_nanopore.fastq > filtered_nanopore.fastq
```
</details>

<details>
<summary>Nanoplot po filtracji</summary>
  
```bash
NanoPlot -t 5 --N50 --fastq filtered_nanopore.fastq -o postfilter_nanoplot
```
</details>



